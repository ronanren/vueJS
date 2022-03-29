<template>
    <h1>Les sorts :</h1>
    <input type="text" id="spell_name_val" v-model="nom">
    <ul>
        <li v-for="spell in spellSearch" :key="spell[1]">
            <SpellView :spell="spell"/>
        </li>
    </ul>
</template>

<script>
import SpellView from './components/SpellView.vue'
import data from './assets/data.min.js'
/* eslint-disable */

export default {
  name: 'App',
  components: {
    SpellView
  },
  data: function() {
      return {
          nom: ""
      }
  },
  computed: {
   spellSearch(){
       return data.filter(spell => spell[1].startsWith(this.nom));
   }
  },
  methods: {
        search : function() {
            
        }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
