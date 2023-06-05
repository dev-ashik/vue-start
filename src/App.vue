<script setup>
import { ref } from "vue";

const showModal = ref(false);
const newNote = ref("");
const errorMessage = ref("");
const notes = ref([]);

const getRandomColor = () => {
  let color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
};

const addNote = () => {
  if(newNote.value.length > 0) {
    notes.value.push({
      id: Math.floor(Math.random() * 10000),
      text: newNote.value,
      date: new Date(),
      bgColor: getRandomColor(),
    });
    showModal.value = false;
    newNote.value = "";
    errorMessage.value = "";
  } else {
    errorMessage.value = "please write something.";
  }

};
</script>

<template>
  <main>
    <div v-show="showModal" class="overlay">
      <div class="modal">
        <textarea
          v-model.trim="newNote"
          name="note"
          id=""
          cols="30"
          rows="10"
        ></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="($event) => (showModal = false)">
          close
        </button>
      </div>
    </div>
    <div class="container">
      <header>
        <!-- {{ notes }} -->
        <h1>Notes</h1>
        <button @click="($event) => (showModal = true)">+</button>
      </header>
      <div class="cars-container">
        <div class="card" v-for="note in notes" :key="note.id" :style="{backgroundColor: note.bgColor}">
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date.toLocaleDateString() }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "App",
};
</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}

.container {
  max-width: 1000px;
  padding: 10px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 100%;
  color: white;
  font-size: 30px;
}

.cars-container {
  display: flex;
  flex-wrap: wrap;
}

.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.date {
  font-size: 12.5px;
  font-weight: bold;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);

  display: flex;
  align-items: center;
  justify-content: center;

  z-index: 10;
}

.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  cursor: pointer;
  margin-top: 15px;
}

.modal .close {
  background-color: rgb(193, 15, 15);
  margin-top: 7px;
}

.modal p {
  color: red;
  margin: 0;
}
</style>
