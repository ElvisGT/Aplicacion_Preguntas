<template>
  <h2>{{ defaultTitle }}</h2>
  <p>{{ count }} <sup>2</sup> = {{ squarerCounter }}</p>
  <button @click="increment">+1</button>
  <button @click="decrement">-1</button>
</template>

<script lang="ts">
export default {
  props:{
    title:String,
    start:{
        type:Number,
        default:10,
        validator( value: number ){
          return value > 0
        }
      },
   
  },
  name: "Counter",
  data() {
    return {
      count: this.start
    }
  },
  methods: {
    increment() {
      this.count += 1;
    },
    decrement() {
      this.count = Math.max(this.count - 1, 0);
    }
  },
  computed: {
    squarerCounter() {
      console.log("Realizado")
      return this.count ** 2;
    },
    defaultTitle(){
      return this.title ? this.title : 'Counter'
    }
  }
}
</script>


<style>
button {
  background-color: #67bb87;
  border-radius: 10px;
  color: white;
  height: 40px;
  margin: 0 5px;
  width: 45px;
}

button:hover {
  cursor: pointer;
}

button:active {
  background-color: yellow;
  transition: ease-in;
}
</style>