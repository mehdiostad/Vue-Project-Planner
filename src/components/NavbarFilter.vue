<template>
  <div class="btns">
    <button @click="updateFilter('all')" :class="{active: current === 'all'}">All</button>
    <button @click="updateFilter('completed')" :class="{active: current === 'completed'}">Completed</button>
    <button @click="updateFilter('ongoing')" :class="{active: current === 'ongoing'}">On Going</button>
  </div>
</template>

<script>
export default {
    props:['current'],
  
methods:{
    updateFilter(by){
        this.$emit('changeFilter',by)
    }
}
}
</script>

<style>
button{
    margin: 5px 20px;
    padding: 20px 30px;
    border: none;
    background: #ddd;
    border-radius: 10px;
    color: white;
    cursor: pointer;
    text-transform: uppercase;
}
.active{
    background: crimson;
}
</style>