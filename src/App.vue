<template>
  <NavBar />
  <router-view />
</template>


<script>

import NavBar from './modules/pokemon/components/NavBar.vue'


export default {
  name: 'App',
  components: {
    NavBar
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;

  text-align: center;
  color: white;
  margin-top: 60px;

}

html,
body {
  background-color: rgba(0, 0, 0, 0);
}

html {
  background: rgba(201, 46, 46, 0.705);
}


button {
  border: 3px solid #adff6a;
  border-radius: 5px;
  background-color: #480aac;
  margin-bottom: 5px;
  cursor: pointer;
  padding: 3px;
  color: white;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif
}

button:hover {
  background-color: rgb(255, 136, 0);
}
</style>
