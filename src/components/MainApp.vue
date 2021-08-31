<template>
  <div class="mainAppDiv">
    <h1>{{ msg }}</h1>
    <GetApp msg="Get Request" :apiURL="apiURL" />
    <PostApp msg="Post Request" :apiURL="apiURL" />
    <PatchApp msg="Patch Request" :apiURL="apiURL" />
  </div>
</template>

<script>
  import GetApp from './GetApp.vue'
  import PostApp from './PostApp.vue'
  import PatchApp from './PatchApp.vue'
  export default {
    name: 'MainApp',
    props: {
      msg: String
    },
    data () {
      return {
        apiURL: 'https://jsonplaceholder.typicode.com',
      }
    },
    components: {
      GetApp,
      PostApp,
      PatchApp
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .mainAppDiv {
    border: 1px solid #000000;
  }
</style>
