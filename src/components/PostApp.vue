<template>
    <div class="PostAppDiv">
        <h1>{{msg}}</h1>
    </div>
</template>

<script>
export default {
  name: 'PostApp',
  props: {
    msg: String
  },
}
</script>

<style scoped>
.PostAppDiv {
    border: 1px dotted #000000;
    margin: 5px;
}
</style>
