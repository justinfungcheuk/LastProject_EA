<template>
<div id="app">
  <div class="container-fluid p-0 m-0 maxWidth">
  <Nav />
  <StaffLogin />
  <router-view/>
  <Footer />
  </div>
</div>
</template>

<script>
import Nav from './components/Nav.vue'
import StaffLogin from '../src/components/login.vue'
import Footer from '../src/components/Footer.vue'

export default {
  name: 'App',
  components: {
    Nav,
    StaffLogin,
    Footer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.header {
  color: red;
  font-weight: bold;
}

.footer {
  position: relative;
  height: 50px;
  font-weight: bold;

}

</style>
