<template>
    <h1>Les sorts :</h1>
    <input type="text" id="spell_name_val" v-model="nom" placeholder="Nom">   
    <input type="checkbox" id="checkbox" v-model="checkedNom">
    <label for="checkbox">recherche active</label>
    <table>
        <tr>
            <th>Nombre de livres</th>
            <th>Nombre de sorts</th>
        </tr>
        <tr>
            <td>{{ statLivre }}</td>
            <td>{{ statSort }}</td>
        </tr>
    </table>
    <table class="table">
        <tr>
            <th>Livre</th>
            <th>Nom</th>
            <th>Sort</th>
            <th>Ecole</th>
            <th>Classe</th>
        </tr>
        <tr v-for="spell in spellSearch" :key="spell[1]">
            <SpellView :spell="spell"/>
        </tr>
    </table>
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
          nom: "",
          checkedNom: false
      }
  },
  computed: {
   spellSearch(){
        if (this.checkedNom)
            return data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()));
        else
            return [];
   },
   statLivre(){
       let value = data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()));
       let count = 0;
       let countArray = [];
       for (const v of value){
           if (!countArray.includes(v[0])){
               count++;
               countArray.push(v[0]);
           }
       } 
        if (this.checkedNom)
            return count;
        else
            return "non défini"
   },
   statSort(){
       let value = data.filter(spell => spell[1].startsWith(this.nom));
       let count = 0;
       let countArray = [];
       for (const v of value){
           if (!countArray.includes(v[2])){
               count++;
               countArray.push(v[0]);
           }
       } 
       if (this.checkedNom)
            return count;
        else
            return "non défini"
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
table {
    margin-top: 25px;
    margin-left: auto;
    margin-right: auto;
}

.table {
    background: white;
    border-radius: 3px;
    border-collapse: collapse;
    margin: auto;
    margin-top: 25px;
    max-width: 1200px;
    padding: 5px;
    width: 100%;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
}
th {
    padding: 5px;
}
.table th {
  color: #D5DDE5;;
  background: #1b1e24;
  border-bottom:4px solid #9ea7af;
  border-right: 1px solid #343a45;
  font-size: 20px;
  font-weight: 100;
  padding: 10px;
  text-align: left;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  vertical-align: middle;
}

.table th:first-child {
  border-top-left-radius: 3px;
}
 
.table th:last-child {
  border-top-right-radius: 3px;
  border-right: none;
}
  
.table tr {
  border-top: 1px solid #C1C3D1;
  border-bottom: 1px solid #C1C3D1;
  color:#666B85;
  font-size:16px;
  font-weight:normal;
  text-shadow: 0 1px 1px rgba(256, 256, 256, 0.1);
}
 
.table tr:hover td {
  background:#4E5066;
  color:#FFFFFF;
  border-top: 1px solid #22262e;
}
</style>
