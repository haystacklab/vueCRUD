<template>
  <div class="PostAppDiv">
      <h1>{{msg}}</h1>
      <div class="postForm">
        <form v-on:submit="submitPostRequest">
          <input />
        </form>
      </div>
  </div>
</template>

<script>
  export default {
    name: 'PostApp',
    props: {
      msg: String
    },
    methods: {
      submitPostRequest (e) {
        e.preventDefault();

      }
    }
  }
</script>

<style scoped>
  .PostAppDiv {
      border: 1px dotted #000000;
      margin: 5px;
  }
</style>
