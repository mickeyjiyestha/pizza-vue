<template>
  <footer>
    <div class="container py-5 border-top border-bottom">
      <div class="footer-flex">
        <div class="footer-col">
          <a href="/" class="d-flex mb-5">
            <img
              src="@/assets/img/logo-alt.svg"
              class="img-fluid"
              alt="Foodnow Logo"
            />
          </a>
          <h4 class="text-primary">Find Us :</h4>
          <div class="social-icons">
            <a href="#" class="btn btn-outline-primary btn-social">
              <img
                src="@/assets/img/facebook.svg"
                class="contact-icon"
                alt=""
              />
            </a>
            <a href="#" class="btn btn-outline-primary btn-social">
              <img
                src="@/assets/img/instagram.svg"
                class="contact-icon"
                alt=""
              />
            </a>
            <a href="#" class="btn btn-outline-primary btn-social">
              <img src="@/assets/img/youtube.svg" class="contact-icon" alt="" />
            </a>
          </div>
        </div>
        <div class="footer-col">
          <h4 class="text-primary">Navigation</h4>
          <ul class="nav-links">
            <li><a href="#" class="nav-link">Home</a></li>
            <li><a href="#" class="nav-link">Order</a></li>
            <li><a href="#" class="nav-link">About</a></li>
            <li><a href="#" class="nav-link">Blog</a></li>
            <li><a href="#" class="nav-link">Contact</a></li>
            <li><a href="#" class="nav-link">Login</a></li>
            <li><a href="#" class="nav-link">Register</a></li>
          </ul>
        </div>
        <div class="footer-col">
          <h4 class="text-primary">Contact</h4>
          <ul>
            <li>
              <img src="@/assets/img/mail.svg" class="contact-icon" alt="" />
              Food.now@mail.com
            </li>
            <li>
              <img src="@/assets/img/phone.svg" class="contact-icon" alt="" />
              +62848477102943
            </li>
            <li>
              <img
                src="@/assets/img/whatsapp.svg"
                class="contact-icon"
                alt=""
              />
              +628184938494
            </li>
          </ul>
        </div>
        <div class="footer-col">
          <h4 class="text-primary">Location</h4>
          <ul class="location">
            <li>
              <img
                src="@/assets/img/location.svg"
                class="contact-icon"
                alt=""
              />
              <div>
                <h5>Kerobokan</h5>
                <p>
                  Jl. Raya Kerobokan Br Taman, Kuta No.98, Kerobokan Kelod, Kec.
                  Kuta Utara, Kabupaten Badung, Bali 80361
                </p>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="container py-3">
      <p class="copyright">
        Copyright © 2022 Foodnow. All Rights Reserved. Powered by PT. Timedoor
        Indonesia. | Privacy Policy This site is protected by reCAPTCHA and the
        Google Privacy Policy and Terms of Service apply.
      </p>
    </div>
  </footer>
</template>

<style scoped>
.footer-flex {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap; /* Allows wrapping on smaller screens */
}

.footer-col {
  flex: 1; /* Each column takes equal space */
  min-width: 200px; /* Minimum width for responsiveness */
  margin-right: 20px; /* Space between columns */
}

.footer-col:last-child {
  margin-right: 0; /* Remove margin from the last column */
}

.copyright {
  text-align: center;
  max-width: 48.5rem;
  margin: auto;
}

.btn-social {
  width: 2.5rem;
  height: 2.5rem;
  padding: 0;
  border-radius: 50%;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  margin-right: 1rem;
}

.btn-social img {
  margin: 0;
}

.btn-social:hover {
  background-color: rgba($color: $primary, $alpha: 0.3) !important;
}

.contact-icon {
  height: 1.25rem;
  width: 1.25rem;
  object-fit: contain;
  margin-right: 0.5rem;
}

footer {
  font-size: 1.125rem;
}

footer h4 {
  margin-bottom: 1.25rem;
}

.nav-links {
  list-style: none;
  padding: 0;
}

.nav-links li {
  margin-bottom: 0.875rem;
}

footer ul {
  list-style: none;
  padding: 0;
}

footer ul li {
  display: flex;
  align-items: center;
  margin-bottom: 0.875rem;
}

.location li {
  align-items: flex-start;
}
</style>
