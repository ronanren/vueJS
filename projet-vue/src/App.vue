<template>
  <h1>Les sorts :</h1>
  <SearchName/>
  <button @click="search">Recherche</button>
  <p></p>
</template>

<script>
import SearchName from './components/SearchName.vue'
import data from './assets/data.min.js'
/* eslint-disable */

export default {
  name: 'App',
  components: {
    SearchName
  },
  mounted(){
    console.log(data);
  },
  methods: {
    search : function() {
        var e = false;
        var b = false;
        var a = "";
        var c = [];
        var f = 0;
        for (var d = 0; d < data.length; d++) {
            e = true;
            e = tableContain([], data[d][0]);
            if (e && document.getElementById("spell_Type_box").checked) {
                e = e && tableContain(sortGetBranches(d), getValue("spell_Type"));
            }
            if (e && document.getElementById("spell_Ecole_box").checked) {
                e = e && sortGetEcole(d) == getValue("spell_Ecole");
            }
            if (e && document.getElementById("spell_Classe_box").checked) {
                e = e && tableContain(sortGetClass(d), getValue("spell_Class"));
            }
            if (e && document.getElementById("spell_name_box").checked) {
                e = e && data[d][1].match(getValue("spell_name_val")) != null;
            }
            if (e && document.getElementById("spell_lvl_box").checked) {
                e = e && tableContain(sortGetLvl(d), parseInt(getValue("spell_lvl")));
            }
            if (e) {
                f++;
                if (document.getElementById("spell_Ecole_box").checked) {
                    c.push(new Array(sortGetClassLvl(d, getValue("spell_Class")), d));
                } else {
                    c.push(new Array(sortGetLvl(d)[0], d));
                }
            }
        }
        if (document.getElementById("spell_cc_box").checked) {
            c.sort();
        }
        for (var d = 0; d < c.length; d++) {
            a += "<div class='panel panel-default'><div class='panel-heading'><h3 class='panel-title' onclick='toggleSort(" + c[d][1] + ");'>" + data[c[d][1]][1] + "</h3></div><div class='panel-body' id='res" + c[d][1] + "'></div></div>";
        }
        document.getElementById("SPELLS").innerHTML = a;
        document.getElementById("count").innerHTML = f;
    }
  }
}
function tableContain(c, b) {
    var a = false;
    for (var d = 0; d < c.length; d++) {
        if (c[d] == b) {
            a = true;
        }
    }
    return a;
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
