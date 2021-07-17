<template>
  <div class="home">
    <section class="netflix">
      <div class="netflix-body">
        <div class="container">
          <h1 class="title">
            Welcome to the Tubeflix !
          </h1>
          <h2 class="subtitle-h2">
            Make sure you check out our upcoming HOT MOVIES below !
          </h2>
        </div>
      </div>
    </section>
    <Films />
  </div>
</template>

<script>

import Films from '../components/Films.vue'

export default {
  name: 'Home',
  components: {
    Films,
  }
}
</script>

<style>
#app {
  height: 100%;
}
.netflix {
  text-align: center;
  background-image: url('https://bingeflix.in/wp-content/uploads/2021/03/Netflix-Background.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 500px;
}

.netflix-body .title {
  text-shadow: 4px 4px 4px rgb(218, 0, 0);
  padding: 40px 0 20px 0;
  font-size: 60px;
  color: red;
}

.subtitle-h2 {
  text-shadow: 4px 4px 4px rgb(218, 0, 0);
  font-size: 30px;
  color: red;
  font-weight: bold;
}

.button-block .button .welcome {
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  position: absolute;
  bottom: -150px;
}
.button {
  margin-right: 50px;
  padding-left: 50px;
  padding-right: 50px;
  font-size: 1.7rem;
}
.welcome {
  width: 400px;
  padding: 10px;
  margin-left: auto;
  margin-right: auto;
}
</style>
