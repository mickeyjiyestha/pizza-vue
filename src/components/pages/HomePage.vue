<template>
  <div class="homepage container">
    <h1 class="title">Choose your pizza</h1>
    <div class="content row">
      <div class="pizza-selection col-lg-8 col-md-12">
        <div
          v-for="pizza in pizzas"
          :key="pizza.id"
          class="pizza-card col-6 col-md-4 col-lg-3"
          :class="{ selected: selectedPizza && selectedPizza.id === pizza.id }"
          @click="selectPizza(pizza)"
        >
          <img
            class="pizza-image"
            :src="getStaticImageSrc(pizza.name)"
            :alt="pizza.name"
          />
          <div class="pizza-info">
            <p>
              <b>{{ pizza.name }}</b>
            </p>
            <p>
              <span v-if="pizza.discount.is_active" class="offer"
                >${{ pizza.price.toFixed(2) }}</span
              >
              <span v-else>${{ pizza.discount.final_price.toFixed(2) }}</span>
            </p>
            <img
              v-if="pizza.discount.is_active"
              src="@/assets/img/ribbon.svg"
              alt="Discount Offer"
              class="discount-logo"
            />
          </div>
        </div>
      </div>

      <div class="payment-summary col-lg-4 col-md-12">
        <h2>Payment Summary</h2>
        <div class="summary-item">
          <span>{{
            selectedPizza ? selectedPizza.name : "Select a pizza"
          }}</span>
          <span
            >${{
              selectedPizza
                ? (selectedPizza.discount.is_active
                    ? selectedPizza.discount.final_price
                    : selectedPizza.price
                  ).toFixed(2)
                : "0.00"
            }}</span
          >
        </div>
        <div class="summary-item">
          <span>Size - {{ selectedSize.name }}</span>
          <span>${{ selectedSize.extra_price.toFixed(2) }}</span>
        </div>
        <div
          v-for="topping in selectedToppings"
          :key="topping.name"
          class="summary-item"
        >
          <span>{{ topping.name }}</span>
          <span>${{ topping.price.toFixed(2) }}</span>
        </div>
        <div class="total-price">
          <span>Total Price</span>
          <span>${{ totalPrice.toFixed(2) }}</span>
        </div>
        <button class="order-button" @click="showModal = true">
          Order Now
        </button>
      </div>

      <!-- Modal -->
      <div v-if="showModal" class="modal-overlay">
        <div class="modal-content">
          <div class="modal-header">
            <h2>Order Success</h2>
          </div>
          <div class="modal-body">
            <img
              src="@/assets/img/cart.gif"
              alt="Cart"
              class="modal-cart-gif"
            />
            <p>Thank you, we have received your order successfully.</p>
          </div>
          <div class="modal-footer">
            <button @click="showModal = false">Close</button>
          </div>
        </div>
      </div>
    </div>

    <h2 class="custom-pizza-title">Custom Pizza</h2>
    <div class="custom-pizza">
      <label>Size</label>
      <div class="size-options">
        <label v-for="size in sizeData" :key="size.id">
          <input
            type="radio"
            name="size"
            :value="size.name"
            :checked="selectedSize.name === size.name"
            @change="selectedSize = size"
          />
          {{ size.name }} (+${{ size.extra_price }})
        </label>
      </div>
    </div>

    <h2 class="toppings-title">Choose Your Toppings</h2>
    <div class="toppings-selection row">
      <div
        v-for="topping in availableToppings"
        :key="topping.id"
        class="topping-checkbox col-6 col-md-4 col-lg-3"
        :class="{
          disabled: !filteredToppings.includes(topping),
          selected: selectedToppings.some((t) => t.id === topping.id),
        }"
        @click="toggleTopping(topping)"
      >
        <input
          type="checkbox"
          :disabled="!filteredToppings.includes(topping)"
          :checked="selectedToppings.some((t) => t.id === topping.id)"
          style="display: none"
        />
        <span>{{ topping.name }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import pizzaData from "@/assets/json/pizza-list.json";
import sizeData from "@/assets/json/size-list.json";
import toppingData from "@/assets/json/topping-list.json";

export default {
  name: "HomePage",
  data() {
    return {
      pizzas: pizzaData.data,
      selectedPizza: null,
      selectedSize: sizeData.data[0], // Default to the first size (Small)
      selectedToppings: [],
      availableToppings: toppingData.data,
      filteredToppings: [], // Toppings available for the selected pizza
      sizeData: sizeData.data, // Add size data to the component's data
      showModal: false,
    };
  },
  computed: {
    totalPrice() {
      const pizzaPrice = this.selectedPizza
        ? this.selectedPizza.discount.is_active
          ? this.selectedPizza.discount.final_price
          : this.selectedPizza.price
        : 0;

      const toppingsPrice = this.selectedToppings.reduce(
        (total, topping) => total + topping.price,
        0
      );

      const sizePrice = this.selectedSize.extra_price; // Get the extra price for the selected size

      return pizzaPrice + toppingsPrice + sizePrice; // Include size price in total
    },
  },
  methods: {
    selectPizza(pizza) {
      this.selectedPizza = pizza;
      this.selectedToppings = []; // Reset toppings when a new pizza is selected
      this.filteredToppings = this.availableToppings.filter(
        (topping) => pizza.toppings.includes(topping.id) // Only include toppings that are available for the selected pizza
      );
    },
    toggleTopping(topping) {
      const index = this.selectedToppings.findIndex((t) => t.id === topping.id);
      if (index === -1) {
        this.selectedToppings.push(topping); // Add topping if not already selected
      } else {
        this.selectedToppings.splice(index, 1); // Remove topping if already selected
      }
    },

    getStaticImageSrc(pizzaName) {
      // Return the static path based on the pizza name
      const formattedName = pizzaName.replace(/\s+/g, "-").toLowerCase(); // Format the pizza name
      return `/src/assets/img/${formattedName}.png`;
    },
  },
};
</script>

<style scoped>
.homepage {
  padding: 20px;
}

.pizza-image {
  width: 100px; /* Atur lebar gambar */
  height: 100%; /* Gambar memenuhi tinggi kartu */
  object-fit: cover; /* Mengisi area gambar tanpa merusak rasio aspek */
  border-radius: 8px; /* Tambahkan border-radius pada gambar */
  margin-right: 10px; /* Jarak antara gambar dan info */
}

.pizza-image:hover {
  transform: rotate(15deg);
}

.topping-checkbox.disabled {
  color: gray; /* Change text color to gray */
  pointer-events: none; /* Prevent interaction */
}

.discount-logo {
  width: 50px; /* Atur lebar logo sesuai kebutuhan */
  height: auto; /* Menjaga rasio aspek */
  position: absolute; /* Agar bisa ditempatkan di atas gambar */
  top: -20px; /* Jarak dari atas */
  left: 100px; /* Jarak dari kiri */
  z-index: 1; /* Pastikan logo di atas gambar */
}

.title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 20px;
}

.content {
  display: flex;
  flex-wrap: wrap; /* Allow wrapping for smaller screens */
}

.pizza-selection {
  display: flex;
  flex-wrap: wrap; /* Allow wrapping for smaller screens */
}

.pizza-card {
  display: flex; /* Mengatur flexbox untuk membuat layout horizontal */
  background-color: #f8f8f8;
  border-radius: 8px;
  padding: 10px;
  align-items: center;
  margin-right: 20px; /* Adjust margin for spacing */
  height: 150px; /* Atur tinggi untuk membuatnya persegi panjang */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  position: relative; /* Untuk menempatkan ribbon */
  overflow: hidden; /* Sembunyikan elemen yang melampaui batas */
}

.pizza-card:hover {
  background-color: rgb(255, 225, 169);
}

.pizza-card.selected {
  background-color: orange; /* Warna latar belakang untuk kartu yang dipilih */
  color: white; /* Warna teks untuk kartu yang dipilih */
}

.pizza-card img {
  width: 100%;
  margin-top: 15px; /* Pastikan gambar memenuhi lebar kartu */
  height: 80px; /* Atur tinggi gambar agar sesuai dengan kartu */
  object-fit: contain; /* Mengisi area gambar tanpa merusak rasio aspek */
  border-radius: 8px; /* Tambahkan border-radius pada gambar */
}

.pizza-info {
  display: flex;
  margin-right: 50px;
  flex-direction: column; /* Mengatur info pizza dalam kolom */
  justify-content: center; /* Pusatkan konten secara vertikal */
}

.pizza-info h2 {
  margin: 0; /* Menghapus margin untuk judul pizza */
}

.pizza-info p {
  margin: 5px 0 0; /* Atur margin untuk paragraf */
}

.offer {
  color: orange;
  text-decoration: line-through;
}

.original {
  color: gray;
}

.custom-pizza-title {
  font-size: 20px;
  margin: 20px 0 10px;
}

.size-options {
  display: flex;
  gap: 20px;
}

.payment-summary {
  background-color: #f8f8f8;
  padding: 15px;
  border-radius: 8px;
}

.summary-item {
  display: flex;
  justify-content: space-between;
  margin: 5px 0;
}

.total-price {
  font-weight: bold;
  margin-top: 10px;
}

.order-button {
  background-color: orange;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 10px;
}

.order-button:hover {
  background-color: darkorange;
}

.toppings-title {
  font-size: 20px;
  margin: 20px 0 10px;
}

.toppings-selection {
  display: flex;
  flex-wrap: wrap; /* Allow wrapping to the next line */
  gap: 10px; /* Space between toppings */
}

.topping-checkbox {
  display: flex;
  align-items: center; /* Center items vertically */
  background-color: #f8f8f8;
  border-radius: 20px; /* Rounded borders */
  padding: 10px;
  cursor: pointer;
  transition: background-color 0.3s;
  width: calc(16.66% - 10px); /* Six items per row with gap */
}

.topping-checkbox.selected {
  background-color: orange; /* Change background color to orange when selected */
  color: white; /* Change text color to white for better contrast */
}

.topping-checkbox:hover {
  background-color: #e0e0e0; /* Change background on hover for better UX */
}

.topping-checkbox input {
  margin-right: 10px; /* Space between checkbox and text */
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5); /* Latar belakang transparan */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000; /* Pastikan modal di atas konten lainnya */
}

.modal-content {
  background-color: white;
  border-radius: 8px;
  padding: 20px;
  width: 300px; /* Atur lebar modal sesuai kebutuhan */
  text-align: center;
}

.modal-header h2 {
  margin: 0;
}

.modal-body {
  margin: 20px 0; /* Jarak antara header dan body */
}

.modal-cart-gif {
  width: 200px; /* Atur lebar gambar sesuai kebutuhan */
  height: 150px; /* Menjaga rasio aspek */
}

.modal-footer {
  margin-top: 20px;
}

.modal-footer button {
  background-color: orange;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
}

.modal-footer button:hover {
  background-color: darkorange;
}

@media (max-width: 768px) {
  .pizza-card {
    width: 100%; /* Mengatur lebar kartu menjadi 100% agar dapat diisi secara horizontal */
    margin-bottom: 20px;
  }

  .discount-logo {
    width: 30px; /* Atur lebar logo sesuai kebutuhan */
    margin-left: 50px;
  }

  .payment-summary {
    margin-top: 20px;
    margin-bottom: 20px;
  }

  .custom-pizza {
    display: block;
  }

  .size-options {
    display: inline-block;
    margin-right: 20px;
  }

  .toppings-selection {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .topping-checkbox {
    width: calc(33.33% - 10px); /* Three items per row with gap */
  }
}
</style>
