<template>
    <h1>Les sorts :</h1>
    <!-- input de recherche par nom -->
    <input type="text" id="spell_name_val" v-model="nom" placeholder="Nom">
    <input type="checkbox" id="checkbox-nom" v-model="checkedNom">
    <label for="checkbox-nom">recherche active</label>

    <!-- input de recherche par livre -->
    <div id="rechercheLivre">
        <input type="text" id="spell_livre_val" v-model="livre" placeholder="Livre">
        <input type="checkbox" id="checkbox-livre" v-model="checkedLivre">
        <label for="checkbox-livre">recherche active</label>
    </div>
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
        <!-- Gestion d'une boucle sur le résultat avec un composant pour afficher chaque spell -->
        <tr v-for="spell in spellSearch" :key="spell[1]">
            <SpellView :spell="spell"/>
        </tr>
    </table>
</template>

<script>
// Import du composant de l'affichage d'un sort
import SpellView from './components/SpellView.vue'
// import des données
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
          livre: "",
          checkedNom: false,
          checkedLivre: false
      }
  },
  computed: {
    // Fonction de recherche avec le tri de configuration active à chaque entrée de caractères
   spellSearch(){
        if (this.checkedNom && this.checkedLivre)
            // Utilisation de la fonction filter pour filtrer les données avec les données commencant par la recherche de l'utilisateur
            return data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()) && spell[0].toLowerCase().startsWith(this.livre.toLowerCase()));
        else if (this.checkedNom)
            return data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()));
        else if (this.checkedLivre){
            return data.filter(spell => spell[0].toLowerCase().startsWith(this.livre.toLowerCase()));
        }
        else
            return [];
   },
   // Fonction permettant de calculer la statistique des livres
   statLivre(){
       // Utilisation de la fonction filter pour filtrer les données avec les données commencant par la recherche de l'utilisateur
        let value = data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()));
        if (this.checkedNom && this.checkedLivre)
            value = data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()) && spell[0].toLowerCase().startsWith(this.livre.toLowerCase()));
        else if (this.checkedNom)
            value = data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()));
        else if (this.checkedLivre)
            value = data.filter(spell => spell[0].toLowerCase().startsWith(this.livre.toLowerCase()));

        let count = 0;
        let countArray = [];
        for (const v of value){
            // ajout des livres dans un tableau et verification des doublons pour compter le nombre de livres différents
            if (!countArray.includes(v[0])){
                count++;
                countArray.push(v[0]);
            }
        } 
        // si au moins une recherche est activé, afficher les statistiques
        if (this.checkedNom || this.checkedLivre)
            return count;
        else
            return "non défini"
   },
   // Fonction permettant de calculer la statistique des sorts
   statSort(){
       // Utilisation de la fonction filter pour filtrer les données avec les données commencant par la recherche de l'utilisateur
        let value = data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()));
        if (this.checkedNom && this.checkedLivre)
            value = data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()) && spell[0].toLowerCase().startsWith(this.livre.toLowerCase()));
        else if (this.checkedNom)
            value = data.filter(spell => spell[1].toLowerCase().startsWith(this.nom.toLowerCase()));
        else if (this.checkedLivre)
            value = data.filter(spell => spell[0].toLowerCase().startsWith(this.livre.toLowerCase()));
       
       let count = 0;
       let countArray = [];
       for (const v of value){
           // ajout des sorts dans un tableau et verification des doublons pour compter le nombre de sorts différents
           if (!countArray.includes(v[2])){
               count++;
               countArray.push(v[0]);
           }
       } 
       // si au moins une recherche est activé, afficher les statistiques
       if (this.checkedNom || this.checkedLivre)
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

#rechercheLivre {
    margin-top: 15px;
}
</style>
