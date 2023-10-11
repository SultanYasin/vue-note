<script>
export default {
  data() {
    return {
      counter: 0,
    };
  },
  methods:{
    increment(){
      this.counter ++
    },
    decrement(){
     this.counter--
    },
  
  }
};
</script>

<template>
  <div>
    <h1>counter is ..</h1>

    <h2 id="cont" >{{ counter < 0 ? "not able": counter }}</h2>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
  </div>
</template>

<style scoped>


</style>
