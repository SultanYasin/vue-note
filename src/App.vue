<template>
  <div>
    <h2>app</h2>
    <input
      type="text"
      @input="setUserName($event, 'xx')"
      @keyup.enter="confInput"
    />
    <p>your name is : {{ confName }}</p>

    <form action="" @submit.prevent>
      <!-- prevent works in same way as preventDefault in JS -->
      <h2>form</h2>
      <h3>the value of the counter is : {{ counter }}</h3>
      <button @click="reduce()">-</button>
      <button @click="add()">+</button>
      <input type="text" name="" id="" />
      <button>submit</button>
    </form>
    <!-- by doing this way I make the backgroundColor changeable according to what written in input   -->
  <input type="text" v-model="bgc" placeholder="colorize the paragraph" >
  <p class="p" :style="{backgroundColor: bgc}" > style me  </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      confName: "",
      counter: 0,
      bgc:''
    };
  },
  methods: {
    subForm() {
      alert("sub");
    },
    setUserName(event, param) {
      this.username = event.target.value + " " + param;
    },
    confInput() {
      this.confName = this.username;
    },
    reduce() {
      this.counter = this.counter - 1;
    },

    add() {
      this.counter = this.counter + 1;
    },
  },

  watch:{
    counter(value){
     if (value > 5) {
      this.counter = 0;
      console.log("counter can not be grater than 5 ")
     }
    }
  },

  computed: {},
  
}
</script>

<style scoped>
div {
  height: 98vh;
  display: flex;
  flex-direction: column;
 /*  justify-content: center; */
  align-items: center;
  background: #000;
  color: white;
}
form {
  display: flex;
  flex-direction: column;
}
input {
  height: 5vh;
}
button {
  font-size: large;
  font-weight: 1000;
  color: black;
}
.p{
  margin-top: 2%;
  height: 100px;
  width: 100px;
  background-color: #fff;
  color: #000;
  text-align: center;

}

</style>
