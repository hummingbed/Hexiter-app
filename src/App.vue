<template>
  <div class="container-fluid p-3">
    <div class="row g-2">

      <div class="col-lg-6 col-md-6 col-sm-12">
        <h2>Hexiter</h2>
        <div class="col d-flex justify-content-center align-items-center my-5 px-5">

          <form @submit.prevent="submitForm">
            <div class="welcome-back text-center">
              <h2>Welcome Back</h2>
              <p>Lets Start off, where we stop</p>
            </div>

            <div class="row gy-3 gy-md-4 px-2 overflow-hidden">
              <div class="col-12">
                <label for="email" class="form-label">Email Address</label>
                <input type="email" class="form-control" name="email" v-model="email" @blur="validateEmail"
                  placeholder="Joan Ben@example.com">
                <span v-if="emailError" style="color: red;">{{ emailError }}</span>
              </div>

              <div class="col-12">
                <label for="password" class="form-label">Password </label>
                <input type="password" class="form-control" placeholder="**********" v-model="password"
                  @blur="validatePassword">
                <span v-if="passwordError" style="color: red;">{{ passwordError }}</span>
                <p class="mt-1">
                  <a href="#!" class="link-secondary text-primary text-decoration-none">Forgot password?</a>
                </p>
              </div>

              <div class="col-12">
                <div class="d-grid">
                  <button :disabled="!isFormValid" type="submit" class="btn btn-primary btn bsb-btn-xl btn-danger">
                    Sign In
                    <div v-if="spinVisiblilty" class="spinner-border text-secondary" role="status"
                      style="width: 1.5rem; height: 1.5rem;">
                      <span class="visually-hidden">Loading...</span>
                    </div>
                  </button>
                  <!-- <button class="btn bsb-btn-xl btn-danger" type="submit">Sign In</button> -->
                </div>
              </div>

              <div class="col-12 text-center">
                <a href="#!" class="text-muted text-decoration-none">Don't have an account? <span
                    class="text-decoration-underline text-danger">Sign Up</span></a>
              </div>

            </div>
          </form>

        </div>
      </div>

      <div class="col-lg-6 col-md-6 col-sm-12 bg-image px-5 d-none d-md-block">
        <div class="row gx-5 right-component">
          <div class="col-12 p-5">
            <div class="ms-4 mt-5">
              <h2 class="fw-bolder">Best Rate</h2>
              <p class="fw-bolder text-muted">We have the best rate among others. <br>
                <span>Our rates are the best in all market-rates</span>
              </p>
            </div>
          </div>
          <div class="col-12 d-flex justify-content-center">
            <div class="cards">
              <img :src="imageFileName" alt="cards">
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>

  <!-- Button trigger modal -->
  <!-- <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
    Launch demo modal
  </button> -->

  <!-- Modal -->

  <!-- <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Api Response</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          {{ apiData }}
        </div>
        
      </div>
    </div>
  </div> -->
</template>

<script>
import cardImage from '@/assets/cards.svg';
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      imageFileName: cardImage,
      email: '',
      password: '',
      emailError: '',
      passwordError: '',
      apiData: "",
      showModal: false,
      spinVisiblilty: false
    };
  },
  methods: {
    validateEmail() {
      if (!this.email) {
        this.emailError = 'Email is required.';
      } else if (!this.isValidEmail(this.email)) {
        this.emailError = 'Please enter a valid email address.';
      } else {
        this.emailError = '';
      }
    },
    validatePassword() {
      if (!this.password) {
        this.passwordError = 'Password is required.';
      } else if (this.password.length < 6) {
        this.passwordError = 'Password must be at least 6 characters long.';
      } else {
        this.passwordError = '';
      }
    },
    isValidEmail(email) {
      // Regular expression for validating email format
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return emailRegex.test(email);
    },
    submitForm() {



      this.spinVisiblilty = true;
      axios.get('http://ip-api.com/json/24.48.0.1')
        .then(response => {
          console.log('Response:', response.data);
          if (response.data.status == 'success') {
            const locationString = `
                country: "${response.data.country}",
                countryCode: "${response.data.countryCode}",
                region: "${response.data.region}",
                regionName: "${response.data.regionName}",
                city: "${response.data.city}",
                zip: "${response.data.zip}",
                lat: ${response.data.lat},
                lon: ${response.data.lon}
              `;
            this.apiData = response.data.status;
            this.$swal.fire({
              title: this.apiData,
              text: locationString,
              $showClass: {
                popup: `
                animate__animated
                animate__fadeInUp
                animate__faster
              `
              },
              $hideClass: {
                popup: `
                animate__animated
                animate__fadeOutDown
                animate__faster
              `
              }
            });


            this.spinVisiblilty = false;
          }
        })
        .catch(error => {
          console.error('Error:', error);
          this.apiData = error;
        });
    }
  },
  computed: {
    isFormValid() {
      return this.email !== '' && this.password.length == 6;
    }
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.bg-image {
  background-image: url('/src/assets/right.svg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: no-repeat;
  height: 96vh;
}

.cards img {
  height: 300px;
  margin-top: 30px;
}

.right-component p {
  font-size: 23px;
}
</style>
