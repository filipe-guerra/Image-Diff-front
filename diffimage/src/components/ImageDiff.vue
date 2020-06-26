<template>
  <div class="comparision">
    <div class="title">
      <h2 class="main_title">First comparision </h2>
      <p> Similarity: {{ img_diff.similarity }} </p>
    </div>
    <div class='img'>
      <img :src="result1_path" name="result_1" v-on:click="greet">
    </div>
    <div class='img'>
      <img :src="result2_path" name="result_2" v-on:click="greet">
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
 
  export default {
    data() {
      return {
        img_diff: [],
        errors: []
      }
    },
  
  methods: {
    greet: function (event) {
      // `this` dentro de métodos aponta para a instância Vue
      alert('Olá ' + event.target.name + '!')
      // `event` é o evento DOM nativo
      // if (event) {
      //   alert(event.target.tagName)
      // }
    }
  },

  // Fetches posts when the component is created.
  created() {

    axios.get('http://127.0.0.1:8000/imagediff')
    .then(response => {
      // JSON responses are automatically parsed.
      console.log(response)
      this.img_diff = response.data
      this.result1_path = require('@/assets/Image-Diff-back/static/result1.png')
      this.result2_path = require('@/assets/Image-Diff-back/static/result2.png')
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.comparision {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.title {
  grid-column: 1 / 3;
}

.main_title {
  color: blue;
}

.img {
  border: 1px solid gray;
  margin: 2px;
}
</style>
