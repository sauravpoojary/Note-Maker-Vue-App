<script>
import { createConditionalExpression } from '@vue/compiler-core';


  export default({

    data(){
      return {
        showModal : false,
        newNote : "",
        notes : []

      }
    },
    methods : {

      addToNote () {
        let noteObj = {
           id : Math.floor(Math.random() * 1000000),
           text : this.newNote,
           date : this.convertDate(new Date())
        };

        this.notes.push(noteObj);
        console.log(this.notes);

        this.showModal = false;
        this.newNote = "";

      },
      convertDate (str) {
        var date = new Date(str),
        mnth = ("0" + (date.getMonth() + 1)).slice(-2),
        day = ("0" + date.getDate()).slice(-2);
        return [date.getFullYear(), mnth, day].join("-");
      }

    }

  })

</script>

<template>
  <main>

    <!-- if showModal is true -->
    <div v-if="showModal" class="overlay">

      <div class="modal">
        <textarea v-model="newNote" name="notes" id="notes" cols="30" rows="10"></textarea>
        <button @click="addToNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>

    </div>
    <div class="container">
      <header>
        <h1>Notes Maker</h1>
        <button @click="showModal = true"><span>+</span></button>
      </header>

      <div class="cards-container">
        <div v-for="note in notes" class="card">

          <p class="main-text">
            {{ note.text }}
          </p>

          <p class="date">
            {{ note.date}}
          </p>

        </div>

      </div>

    </div>

  </main>
</template>

<style scoped>

  main{
    height : 100vh;
    width : 100vw;
    background-color: rgb(0, 255, 136);
  }

  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 35px;
  }

  h1{
    font-weight: bold;
    font-size: 55px;
  }

  span{
    color: white;
  }
  header button{
    border: none;
    padding: 15px;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    cursor: pointer;
    background-color: rgb(44,62,80);
    font-size: 20px;
  }

  .modal{
    width: 700px;
    background-color: rgb(0, 255, 136);;
    border-radius: 10px;
    position: relative;
    padding: 30px;
    display: flex;
    flex-direction: column;
  }

  .modal button {
    padding: 10px 10px;
    font-size: 20px;
    width: 100%;
    background-color: rgb(44,62,80);
    color: white;
    border: none;
    cursor: pointer;
    margin-top: 10px;
  }

  .card{
    width: 200px;
    height: 200px;
    background-color: rgb(44,62,80);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 30px;
    margin-bottom: 30px;
  }

  p{
    color: white;
  }

  .date{
    font-size: 15px;
    font-weight: bold;
  }

  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }

  .overlay{
    position: absolute;
    background-color: rgb(0,0,0,0.77);
    width: 100%;
    height: 100%;
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
 
  }

  .modal .close{
    background-color: rgb(187, 3, 3);
  }
</style>
