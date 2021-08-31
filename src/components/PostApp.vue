<template>
  <div class="PostAppDiv">
      <h1>{{msg}}</h1>
      <div class="postForm">
        <form v-on:submit="submitPostRequest">
          <input v-model="username" placeholder="username" /> <br>
          <button type="submit">Submit Post Data</button>
        </form>
        <div class="responseDiv" v-if="dataSaved">
          Your username has been saved with id: {{ id }}
        </div>
      </div>
  </div>
</template>

<script>
  export default {
    name: 'PostApp',
    props: {
      msg: String,
      apiURL: String
    },
    data () {
      return {
        username: '',
        dataSaved: false,
        id: null,
      }
    },
    methods: {
      submitPostRequest (e) {
        e.preventDefault();
        if (!this.username) {
          alert('please provide the username to save your data')
          return null;
        }
        fetch(this.apiURL + '/posts', {
          method: "POST",
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({username: this.username})
        })
        .then(function(resp) {return resp.json()})
        .then(this.showResp)
      },
      showResp (data) {
        if (data && data.id && data.username) {
          this.dataSaved = true;
          this.id = data.id;
          setTimeout(function() {
            this.dataSaved = false;
          }, 2500)
        }
      },
    }
  }
</script>

<style scoped>
  .PostAppDiv {
    border: 1px dotted #000000;
    margin: 5px;
  }
</style>
