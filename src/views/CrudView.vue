<script>
export default {
  data(){
    return {
      
    }
  },
  computed: {

  },
  watch: {

  },
  methods: {
    create(){

    },
    update(){

    },
    delete(){

    }
  }
}
</script>

<template>
  <div class="about">
    <h1>This is an crud page</h1>
    <label>Name: <input v-model="first"></label>
  <label>Surname: <input v-model="last"></label>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>