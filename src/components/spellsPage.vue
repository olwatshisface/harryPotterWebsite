<template>
  <div>
    <h1>Spells</h1>
    <table v-if="spells.length > 0" id="spells">
      <tr>
        <th v-for="{display} in spellKeysAndTableHeaders" :key="display">{{display}}</th>
      </tr>
      <tr></tr>
      <tr v-for="spell in spells" :key="spell._id">
        <td v-for="{value} in spellKeysAndTableHeaders" :key="value">{{spell[value]}}</td>
      </tr>
    </table>
    <h2 class="error" v-if="errored">There was a problem retreiving the spells</h2>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "spellsPage",
  props: {
    apiKey: String,
  },
  data() {
    return {
      spells: [],
      spellKeysAndTableHeaders: [
        { value: "spell", display: "Spell" },
        { value: "type", display: "Type" },
        { value: "effect", display: "Effect" },
      ],
     errored: false,
    };
  },
  //get spell information as soon in the lifecycle as possible
  mounted() {
    axios
      .get("https://www.potterapi.com/v1/spells?key=" + this.apiKey)
      .then((response) => this.spells = response.data)  
      .catch(e => { 
      console.log(e);  
      this.errored = true;
    });
  },
};
</script>

<style scoped>
/* this could be a mixin it's the same for all 3 pages */
#spells {
  font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  max-width: 100%;
}

#spells td,
th {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

#spells tr:nth-child(even) {
  background-color: #f2f2f2;
}

#spells tr:hover {
  background-color: #ddd;
}

#spells th {
  padding-top: 12px;
  padding-bottom: 12px;
  background-color: #7c807c;
  color: white;
}

.error {
  font-weight: bold;
  color:red;
}
</style>
