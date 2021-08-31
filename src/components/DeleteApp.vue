<template>
  <div class="deleteApp">
    <h1>{{msg}}</h1>
    <div class="deleteForm">
      <form v-on:submit="submitGetRequest">
        <input v-model="id" placeholder="Enter ID"/> <br>
        <button type="submit">Get Data to delete</button>
      </form>
    </div>
    <div class="responseDiv" v-if="showDataBool">
      <p>ID: {{fetchedObj.id}}</p>
      <p>userID: {{fetchedObj.userId}}</p>
      <p>title: {{fetchedObj.title}}</p>
      <p>body: {{fetchedObj.body}}</p>
      <button v-on:click="deleteItem">Confirm Delete?</button>
    </div>
    <div class="deleteResp" v-if="showDeleteRespBool">
      <p>The selected item has been deleted</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DeleteApp',
  props: {
    msg: String,
    apiURL: String
  },
  data () {
    return {
      showDataBool: false,
      showDeleteRespBool: false,
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
    deleteItem (e) {
      e.preventDefault();
      fetch(this.apiURL + '/posts/' + this.fetchedObj.id, {
         method: "DELETE",
      })
      .then(function(resp) { return resp.json()})
      .then(this.showDeleteResp)
    },
    showDeleteResp () {
     this.showDeleteRespBool = true;
     this.showDataBool = false;
    }
  }
  
}
</script>
