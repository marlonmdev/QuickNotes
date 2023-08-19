<script setup>
  import { ref } from "vue"
  
  const showModal = ref(false)
  const notes = ref([])
  const newNoteTitle = ref("")
  const newNoteText = ref("")
  const errorMessage = ref("")
  
  const getRandomColor = () => {
    return "hsl(" + Math.random() * 360 +", 100%, 75%)";
  }
  
  const addNote = () => {
    if(newNoteText.value.length < 8){ 
      return errorMessage.value = "Note must be 8 characters or More!!"
    }
    
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      title: newNoteTitle.value,
      text: newNoteText.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    })
    
    showModal.value = false
    newNoteTitle.value = ""
    newNoteText.value = ""
    errorMessage.value = ""
  }
  
  const closeModal = () => {
    showModal.value = false
    newNoteTitle.value = ""
    newNoteText.value = ""
    errorMessage.value = ""
  }
  
</script>

<template>
  <main> 
    
    <div v-show="showModal" class="modal-overlay">
      <div class="modal">
        <input v-model.trim="newNoteTitle" type="text" name="title" placeholder="Enter Note Title..">
        <textarea v-model.trim="newNoteText" name="notes" id="notes" cols="30" rows="12" placeholder="*Enter Note Here.."></textarea>
        <p class="error" v-if="errorMessage">{{ errorMessage }}</p>
        <div class="btn-container"> 
          <button @click="addNote" class="btn-add">Add Note</button>
          <button @click="closeModal" class="btn-close">Close</button>
        </div>
      </div>
    </div>
    
    <div class="container">
      <header>
        <h1>QuickNotes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: note.backgroundColor}">
          <h4 class="note-title">{{ note.title }}</h4>
          <p class="note-text">
            {{ note.text }}
          </p>
          <p class="note-date">
            🕒 {{ note.date.toLocaleDateString("en-US") }}
          </p>
        </div>  
      </div>
    </div>
  </main>
</template>

<style scoped>
  main {
    background-color: rgb(9, 16, 19);
    min-height: 100vh;
    width: 90vw;
    overflow: hidden;
    font-family: monospace, sans-serif;
  }
  
  .container {
    max-width: 800px;
    padding: 10px;
    margin: 0 auto;
  }
  
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  h1 {
    color: #fffef1;
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 50px;
  }
  
  header button {
    border: none;
    padding: 10px;
    height: 50px;
    width: 50px;
    cursor: pointer;
    background-color: rgb(40, 111, 241);
    border-radius: 50%;
    color: #ffff;
    font-size: 20px;
    box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
  }
  
  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }
  .card {
    min-height: 225px;
    width: 225px;
    padding: 10px;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
  }
  
  .note-title {
    text-transform: uppercase;
  }
  .note-text {
    text-align: justify;
  }
  
  .note-date {
    font-size: 14px;
    font-weight: bold;
    text-align: left;
    padding: 10px 0;
  }
  
  .modal-overlay {
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    z-index: 10;
  }
  
  .modal {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: 750px;
    background-color: #fffef1;
    border-radius: 10px;
    padding: 30px;
    position: relative;
  }
  
  .modal .btn-container{
    display: flex;
    justify-content: flex-end;
    margin-top: 20px;
    gap: 20px;
  }
  
  .modal .btn-add, .btn-close  {
    padding: 15px 30px;
    font-size: 20px;
    width: 180px;
    background-color: rgb(29, 219, 124);
    border: none;
    color: #ffff;
    cursor: pointer;
    box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
  }
  
  .btn-close {
    background-color: rgb(42, 59, 51);
  }
  
  input {
    border-radius: 10px;
    padding: 10px;
    font-size: 20px;
    margin-bottom: 20px;
    border: 2px solid rgb(9, 16, 19);
  }
  
  textarea {
    border-radius: 10px;
    padding: 10px;
    font-size: 20px;
    border: 2px solid rgb(9, 16, 19);
  }
  
  .error {
    margin-top: 8px;
    font-size: 18px;
    color: #e73c25;
    font-weight: bold;
  }
</style>
