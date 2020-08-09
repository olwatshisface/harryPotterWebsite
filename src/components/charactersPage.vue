<template>
  <div>
    <h1>Characters</h1>
    <table v-if="characters.length > 0" id="characters">
      <tr>
        <th v-for="{display} in characterKeysAndFormatterHeaders" :key="display">{{display}}</th>
      </tr>
      <tr></tr>
      <tr v-for="character in characters" :key="character._id">
        <td v-for="{value} in characterKeysAndFormatterHeaders" :key="value">{{character[value]}}</td>
      </tr>
    </table>
    <h1 class="error" v-if="errored">There was a problem retreiving the characters</h1>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "CharactersPage",
  props: {
    apiKey: String,
    houseName: String,
  },
  data() {
    return {
      characters: [],
      characterKeysAndFormatterHeaders: [
        { value: "name", display: "Name" },
        { value: "house", display: "House" },
        { value: "patronus", display: "Patronus" },
        { value: "species", display: "Species" },
        { value: "bloodStatus", display: "Blood Status" },
        { value: "role", display: "Role" },
        { value: "school", display: "School" },
        { value: "deathEater", display: "Death Eater?" },
        { value: "dumbledoresArmy", display: `Dumbledore's Army?` },
        { value: "orderOfThePhoenix", display: "Order Of The Phoenix?" },
        { value: "ministryOfMagic", display: "Ministry Of Magic?" },
        { value: "alias", display: "Alias" },
        { value: "wand", display: "Wand" },
        { value: "boggart", display: "Boggart" },
        { value: "animagus", display: "Animagus" },
      ],
      errored: false,
    };
  },
  mounted() {
    const url =
    // if on the house page get characters by house name
      this.houseName
        ?
         "https://www.potterapi.com/v1/characters?key=" + this.apiKey + "&house=" + this.houseName
        :
        "https://www.potterapi.com/v1/characters?key=" + this.apiKey;
    axios.get(url)
    .then((response) => this.characters = response.data)
    .catch(e => { 
      console.log(e);  
      this.errored = true;
    });
  },
};
</script>

<style scoped>
/* this could be a mixin it's the same for all 3 pages */
#characters {
  font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  max-width: 100%;
}

#characters td,
#characters th {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

#characters tr:nth-child(even) {
  background-color: #f2f2f2;
}

#characters tr:hover {
  background-color: #ddd;
}

#characters th {
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
