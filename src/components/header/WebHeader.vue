<template>
  <header class="header">
    <nav class="navbar navbar-expand-lg navbar-dark">
      <div class="container-fluid me-5">
        <div class="navbar-brand">
          <img src="@/assets/img/logo.svg" alt="" style="padding-left: 25px" />
        </div>
        <button
          class="navbar-toggler"
          type="button"
          @click="toggleMenu"
          aria-controls="navbarNav"
          aria-expanded="isMenuActive"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div
          class="collapse navbar-collapse"
          :class="{ show: isMenuActive }"
          id="navbarNav"
        >
          <div class="navbar-nav mx-auto">
            <a class="nav-link" href="#">Home</a>
            <a class="nav-link" href="#">Order</a>
            <a class="nav-link" href="#">Blog</a>
            <a class="nav-link" href="#">About</a>
            <a class="nav-link" href="#">Contact us</a>
          </div>
          <div class="navbar-nav">
            <a class="nav-link mx-auto mx-auto" href="#">Login</a>
            <a
              class="btn btn-primary me-1"
              style="background-color: orange; border: none"
              href="#"
              >Register</a
            >
          </div>
        </div>
      </div>
    </nav>
    <div class="header-content">
      <p class="header-title"><b>Pizza Order</b></p>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      isMenuActive: false,
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuActive = !this.isMenuActive;
    },
  },
};
</script>

<style scoped>
@keyframes slideIn {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.header-title {
  font-size: 80px;
  color: orange;
  text-align: center;
  animation: slideIn 1s ease forwards;
}

.header {
  background-image: url("@/assets/img/hero.png");
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-top: 20px;
  animation: fadeIn 1s ease forwards;
}

.header-content {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.header-title {
  font-size: 80px;
  color: orange;
  text-align: center;
}

.nav-link {
  color: orange;
  font-size: 20px;
}

.nav-link:hover {
  color: white;
}

@media (max-width: 768px) {
  .header-title {
    font-size: 50px;
  }

  .navbar-nav {
    margin: auto;
    margin-top: 20px;
    align-items: center;
    justify-content: center;
  }

  .nav-link {
    text-align: center;
  }

  .navbar-nav.ms-auto {
    margin-top: 10px;
  }
}

.header-content h1 {
  color: white;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}
</style>
