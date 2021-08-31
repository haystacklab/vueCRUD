<template>
  <div class="PatchAppDiv">
    <h1>{{msg}}</h1>
    <div class="patchForm">
      <form v-on:submit="submitGetRequest">
        <input v-model="id" placeholder="Enter ID"/> <br>
        <button type="submit">Get Data to edit</button>
      </form>
      <div class="responseDiv" v-if="showDataBool">
        <p>Please edit the following fields where you want to</p>
        <form v-on:submit="submitPatchRequest">
          <input v-model="fetchedObj.id" disabled="disabled" /> <br>
          <input v-model="fetchedObj.userId" disabled="disabled" /> <br>
          <input v-model="fetchedObj.title" /> <br>
          <input v-model="fetchedObj.body" /> <br>
          <button type="submit">Update data</button>
        </form>
      </div>
      <div class="showResp" v-if="dataUpdated">
        <p>Your data has been updated. Your updated data:</p>
        <p>Title: {{fetchedObj.title}}</p>
        <p>Body: {{fetchedObj.body}}</p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'PatchApp',
    props: {
      msg: String,
      apiURL: String
    },
    data () {
      return {
        username: '',
        dataUpdated: false,
        showDataBool: false,
        id: null,
        fetchedObj: {
          id: null,
          userId: null,
          title: '',
          body: ''
        }
      }
    },
    methods: {
      submitGetRequest (e) {
        e.preventDefault();
        if (!this.id) {
          alert('please provide id')
          return null;
        }
        fetch(this.apiURL + '/posts/' + this.id)
        .then(function(resp) {return resp.json()})
        .then(this.showData)
      },
      showData (data) {
        if (data && data.id) {
          this.showDataBool = true;
          this.fetchedObj = Object.assign(this.fetchedObj, data)
        }
      },
      submitPatchRequest (e) {
        e.preventDefault();
        if (!this.fetchedObj.id || !this.fetchedObj.userId || !this.fetchedObj.title || !this.fetchedObj.body) {
          alert('Please enter all the fields to continue')
          return null;
        }
        fetch(this.apiURL + '/posts/' + this.fetchedObj.id, {
          method: "PATCH",
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.fetchedObj)
        })
        .then(function(resp) {return resp.json()})
        .then(this.showResp)
      },
      showResp (data) {
        if (data.id) {
          this.dataUpdated = true;
          this.fetchedObj = Object.assign(this.fetchedObj, data)

        }
      }
    }
  }
</script>

<style scoped>
  .PatchAppDiv {
    border: 1px dotted #000000;
    margin: 5px;
  }
</style>
