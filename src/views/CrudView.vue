<script>
export default {
  data(){
    return {
      all_names: [
        {First: "Emil", Last: "Hans"},
        {First: "Mustermann", Last: "Max"},
        {First: "Tisch", Last: "Roman"},
      ],
      selected_name: '',
      current_first: '',
      current_last: '',
      search_key: '',
    }
  },
  computed: {
    filteredNames() {
      return this.all_names.filter((name) => name.First.indexOf(this.search_key)>-1 || name.Last.indexOf(this.search_key) >-1)
    }
  },
  watch: {
    selected_name(newSelected){
      this.current_first = this.all_names.filter((name) => name.First + " " + name.Last == newSelected)[0].First;
      this.current_last = this.all_names.filter((name) => name.First + " " + name.Last == newSelected)[0].Last;
    }
  },
  methods: {
    create(){
      this.all_names.push({First: this.current_first, Last: this.current_last});
    },
    update(){
      this.all_names.map((name, index)=>{
        if(name.First + " " + name.Last == this.selected_name){
          this.all_names[index].First = this.current_first
          this.all_names[index].Last = this.current_last
          this.selected_name = this.current_first + " " + this.current_last
          return
        }
      })
    },
    del(){
      this.all_names = this.all_names.filter((name) => name.First + " " + name.Last != this.selected_name)
      this.current_first = ''
      this.current_last = ''
    }
  },
}
</script>

<template>
  <div class="about">
    <h1>This is an crud page</h1>
    <div class="searchs">
      <input v-model="search_key" placeholder="search names here">
    </div>
    <div class="selects">
      <select size="10" v-model="selected_name">
        <option v-for="name in filteredNames" :key="name.id">
          {{ name.First + " " + name.Last}}
        </option>
      </select>
    </div>
    <div class="inputs">
      <input v-model="current_first" placeholder="First Name">
      <input v-model="current_last" placeholder="Last Name">
    </div>
    <div class="buttons">
      <button @click="create">Create</button>
      <button @click="update">Update</button>
      <button @click="del">Delete</button>
    </div>
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
* {
  font-size: inherit;
}

input {
  display: block;
  margin-bottom: 10px;
}

select {
  float: left;
  margin: 0 1em 1em 0;
  width: 14em;
}

.buttons {
  clear: both;
}

button + button {
  margin-left: 5px;
}
</style>