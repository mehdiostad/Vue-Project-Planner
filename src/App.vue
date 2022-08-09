<template>
<Navbar/>
<router-view/>
</template>
<script>
import Navbar from './components/Navbar.vue';
export default {
  components:{
    Navbar
  }

};
</script>
<style>
body {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 0 auto;
  max-width: 600px;
  color: #554;

}
</style>
