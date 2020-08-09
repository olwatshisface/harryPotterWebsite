<template>
  <div>
    <h1>Characters</h1>
    <table v-if="characters.length > 0" id="characters">
      <tr>
        <th v-for="{display} in tableHeadersAndCharacterKeys" :key="display">{{display}}</th>
      </tr>
      <tr></tr>
      <tr v-for="character in characters" :key="character._id">
        <td v-for="{value} in tableHeadersAndCharacterKeys" :key="value">{{character[value]}}</td>
      </tr>
    </table>
    <h2 class="error" v-else>There was a problem retreiving the characters</h2>
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
      //this needs a new name
      tableHeadersAndCharacterKeys: [
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
    };
  },
  mounted() {
    //add catch to display error
    console.log(this.houseName);
    const url =
      this.houseName
        ?
         "https://www.potterapi.com/v1/characters?key=" + this.apiKey + "&house=" + this.houseName
        :
        "https://www.potterapi.com/v1/characters?key=" + this.apiKey;
        console.log(url);
    axios.get(url).then((response) => this.characters = response.data);
  },
};
</script>

<style scoped>
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
  background-color: #4caf50;
  color: white;
}
</style>
