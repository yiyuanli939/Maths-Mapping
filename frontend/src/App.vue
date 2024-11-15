<!-- frontend/src/App.vue -->

<template>
  <div id="app">
    <h1>Mindmap with LaTeX Support</h1>
    <button @click="pingBackend">Ping Backend</button>
    <p>{{ message }}</p>
    <katex-element :expression="latexExpression" />
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      latexExpression: '\\int_{a}^{b} x^2 dx',
      message: ''
    }
  },
  methods: {
    async pingBackend() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/ping')
        this.message = response.data.message
      } catch (error) {
        this.message = 'Error connecting to backend'
        console.error(error)
      }
    }
  }
}
</script>

<style>
/* Add any custom styles here */
#app {
  text-align: center;
  margin-top: 50px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  margin-bottom: 20px;
  cursor: pointer;
}

p {
  font-size: 18px;
  color: #333;
}
</style>

