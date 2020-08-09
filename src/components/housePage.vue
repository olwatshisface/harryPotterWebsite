<template>
  <div>
    <div v-if="selectedHouse">
      <h1>{{selectedHouse.name}}</h1>
      <table id="house">
        <tr>
          <th v-for="{display} in houseKeysandFormattedHeaders" :key="display">{{display}}</th>
        </tr>
        <tr></tr>
        <tr v-for="house in houses" :key="house._id">
          <td v-for="{value} in houseKeysandFormattedHeaders" :key="value">{{house[value]}}</td>
        </tr>
      </table>
      <CharactersPage :house-name="selectedHouse.name" :api-key="apiKey" />
    </div>
    <h2 class="error" v-if="errored">There was a problem retreiving the House</h2>
  </div>
</template>
<script>
import CharactersPage from "./charactersPage";
import axios from "axios";

export default {
  name: "housePage",
  components: {
    CharactersPage,
  },
  props: {
    selectedHouse: Object,
    apiKey: String,
  },
  data() {
    return {
      houses: [],
      houseKeysandFormattedHeaders: [
        { value: "mascot", display: "Mascot" },
        { value: "headOfHouse", display: "Head Of House" },
        { value: "houseGhost", display: "House Ghost" },
        { value: "founder", display: "Founder" },
        { value: "school", display: "School" },
        { value: "values", display: "Values" },
        { value: "colors", display: "Colors" },
      ],
      errored: false,
    };
  },
  methods: {},
  created() {
    axios
      .get("https://www.potterapi.com/v1/houses/" + this.selectedHouse._id + "?key=" + this.apiKey)
      .then((response) => this.houses = response.data) 
      .catch(e => { 
      console.log(e);  
      this.errored = true;
    });
  },
};
</script>

<style scoped>
#house {
  font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  max-width: 100%;
}

#house td,
th {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

#house tr:nth-child(even) {
  background-color: #f2f2f2;
}

#house tr:hover {
  background-color: #ddd;
}

#house th {
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
