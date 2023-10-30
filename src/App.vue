<template>
  <div class="container">
    <h1>Goals</h1>
    <div class="input">
      <input
        type="text"
        placeholder="write your goals here to add into the list"
        v-model="enteredValue"
      />
      <button @click="addGoal">add goal</button>

    </div>
      <div class="goals">
        <p v-if="goals.length == 0 " >no goals, add some</p>
        <p v-else > <ul><li v-for=" (goal, index ) in goals" :key="index" @click="showID" class="li" > {{goal}} - {{index}} - <button @click="removeGoal(index)" >del</button> </li></ul> </p>
      </div>

   
  </div>
</template>

<script>
export default {
  data() {
    return {
      enteredValue : "",
      goals: [],

    };
  },
  methods: {
    addGoal() {
      this.goals.push(this.enteredValue)
      console.log(this.goals.length)
      this.enteredValue = "";
    },
    removeGoal(ele_index){
      this.goals.splice(ele_index, 1)
    },
 

  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.input {
  display: flex;
  margin-bottom: 10px;
}

.li{
  background-color: lightgray;
  width: 250px;
  border-radius: 50px;
  text-align: center;
}
li button{
  margin-left: 20px;
  width: 40px;
  border-radius: 20px;
}
</style>
