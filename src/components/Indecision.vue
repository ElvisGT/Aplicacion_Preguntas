<template>
  <img v-if="image" :src="image" alt="bg">  
  <div class="bg-dark"></div>
  
  <div class="indecision-container">
    <input v-model="question" type="text" placeholder="Haz una pregunta">
    <p>Recuerda terminar con signo de interrogación (?)</p>

    <div v-if="isValidQuestion">
      <h2>{{ question }}</h2>
      <h1>{{ answer }}</h1>
    </div>
  </div>
</template>

<script lang="ts">
  import type { DataApi } from '../interfaces/dataAPI';

  export default {
    name:"Indecision",
    data(){
      return {
        question:'',
        answer:'',
        image:'',
        isValidQuestion:false
      }
    },
    methods:{
      async getAnswer(){
        this.answer = "...Pensando";

        const data = await fetch('https://yesno.wtf/api')
        const {answer,image}: DataApi = await data.json();  
        this.answer = (answer === 'yes' ? 'Si!' : 'No!');
        this.image = image ;    
      }
    },
    watch:{
      question(value: string){
        this.isValidQuestion = false;

        if(!value.includes("?")) return;

        this.isValidQuestion = true;

        this.getAnswer();
      }
    }
    
  }
</script>

<style scoped>
    img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);

    }

    .indecision-container {
      width: 100vw;
      margin-top: 150px;
      align-items: center;
      display: flex;
      flex-direction: column;
      z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>