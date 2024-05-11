<template>
  <div class="container-fluid p-3">
    <div class="row g-2">
      
      <div class="col-lg-6 col-md-6 col-sm-12">
        <h2>Hexiter</h2>
        <div class="col d-flex justify-content-center align-items-center my-5 px-5">

          <form action="#!">
            <div class="welcome-back text-center">
              <h2>Welcome Back</h2>
              <p>Lets Start off, where we stop</p>
            </div>
  
            <div class="row gy-3 gy-md-4 px-2 overflow-hidden">
              <div class="col-12">
                <label for="email" class="form-label">Email Address</label>
                <input type="email" class="form-control" name="email" id="email" placeholder="Joan Ben@example.com"
                  required>
              </div>

              <div class="col-12">
                <label for="password" class="form-label">Password </label>
                <input type="password" class="form-control" name="password" placeholder="**********" id="password" value="" required> <br>
                <a href="#!" class="link-secondary text-primary text-decoration-none">Forgot password?</a>
              </div>
             
              <div class="col-12">
                <div class="d-grid">
                  <button class="btn bsb-btn-xl btn-danger" type="submit">Sign In</button>
                </div>
              </div>

              <div class="col-12 text-center">
                <a href="#!" class="text-muted text-decoration-none">Don't have an account? <span class="text-decoration-underline text-danger">Sign Up</span></a>
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
              <img :src="imageFileName" alt="My Image">
              <!-- <img :src="myImage" alt="cards"> -->
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import myImage from '@/assets/cards.svg';

export default {
  name: 'App',
  data() {
    return {
      imageFileName: myImage,
    };
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
