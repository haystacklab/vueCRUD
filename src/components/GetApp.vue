<template>
  <div class="GetAppDiv">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{user.name}} <b>Ph:</b>{{user.phone}}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'GetApp',
    props: {
      msg: String
    },
    data () {
      return {
        users: [],
      }
    },
    methods: {
      async getData () {
        fetch('https://jsonplaceholder.typicode.com/users')
        .then(function (response) { return response.json() })
        .then(this.setResults)
      },
      setResults (data) {
          console.log(data)
          this.users = data;
      }
    },
    created () {
      this.getData()
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .GetAppDiv {
      border: 1px dotted #000000;
      margin: 5px;
  }
</style>