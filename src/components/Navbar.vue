<template>
  <div class="main-nav">
    <router-link :to="{name:'home'}">Projects</router-link>
    <router-link :to="{name:'AddProject'}">Add New Project</router-link>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.main-nav{
    margin: 40px auto;
    text-align: center;
}
.main-nav a{
    margin: 0px 20px;
    text-decoration: none;
    display: inline-block;
    color: #999;
    font-size: 18px;
    text-transform: uppercase;
}
a.router-link-active {
   border-bottom: 2px solid rgb(0, 214, 0);
   padding-bottom: 4px;
}
</style>