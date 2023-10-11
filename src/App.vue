<script setup>
import { format } from "date-fns";
import { ref } from "vue";

let showModal = ref(true);
let newNote = ref("");
let notes = ref([]);
let errMsg = ref("")

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

function closeModalAfterAddingNote() {
  showModal.value = false;
  newNote.value = "";
}

const addNote = () => {
  let id = 0;

  if (newNote.value.length > 6) {
    notes.value.push({
      id: ++id,
      text: newNote.value,
      date: new Date().toLocaleDateString(),
      backgroundColor: getRandomColor(),
    });

    closeModalAfterAddingNote();
  } else return errMsg.value = "Note has to be at least 6 chr ";
};
</script>
<!-- by doing this -> v-model.trim="newNote" I prevent the user from entering an empty spaces and it will not be counted as a value  -->
<template>
  <main>
    <section class="modal" v-if="showModal">
      <div class="modal-div">
        <textarea
          v-model.trim="newNote" 
          name="noteText"
          id="noteText"
          cols="40"
          rows="8"
          placeholder="write your note ..."
        ></textarea>
        <p v-if="errMsg" > {{errMsg}} </p>
        <button class="add" @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">close</button>
      </div>
    </section>
    <header>
      <h1>Add your Notes here</h1>
      <button class="add-btn" @click="showModal = true">+</button>
    </header>
    <body>
      <div class="card-container">
        <div
          v-for="note in notes"
          class="card"
          :style="{ backgroundColor: note.backgroundColor }"
          :key="note.id"
        >
          <h3 class="title">{{ note.text }}</h3>
          <div class="modify">
            <p class="date">{{ note.date }}</p>
            <button class="delete">delete</button>
          </div>
          <!--  <p class="date"> {{currentDateTime}} </p> -->
        </div>
      </div>
    </body>
  </main>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>

<style scoped>

main {
  height: 90vh;
  width: 90vw;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: rgb(21, 20, 20);
  margin: 5%;
}

.add-btn {
  width: 50px;
  height: 50px;
  border-radius: 30%;
  background-color: rgb(21, 20, 20);
  font-size: 2rem;
  color: white;
  cursor: pointer;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
}

.card {
  background-color: lightgoldenrodyellow;
  height: 200px;
  width: 250px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  padding: 10px;
  margin: 1%;
  overflow: auto;
}

.title {
  margin: 20px auto 10px;
}
.modify {
  margin-top: auto;
  display: flex;
  justify-content: space-between;
}
.date {
  font-weight: bold;
  font-size: 14px;
  text-align: left;
  margin-top: auto;
  text-decoration: underline;
}
.delete {
  width: 60px;
  margin-top: auto;
  border-radius: 20px;
  cursor: pointer;
}

.modal {
  position: absolute;
  z-index: 10;
  width: 98%;
  height: 98%;
  background-color: rgba(0, 0, 0, 0.77);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-div {
  width: 700px;
  background-color: #fff;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.add {
  background-color: blueviolet;
  margin: 10px 0;
  height: 30px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
}
.close {
  background-color: red;
  height: 30px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
}
</style>
