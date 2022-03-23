<template>
  <div id="search-form">
    <p>Search Name :</p>
    <input type="text" id="spell_name_val">
    <input type="checkbox" id="spell_name_box" value="Recherche Par Ecole">
  </div>
</template>

<script>
export default {
  name: 'SearchName'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#search-form {
  display: flex;
  align-items: center; 
  justify-content: center;
}
#search-form > p {
  margin-right: 10px;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
