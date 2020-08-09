<template>
  <div id="app">
    <a href="https://logo-logos.com/harry-potter-logo-610.html">
      <img
        src="https://logo-logos.com/wp-content/uploads/2016/10/Harry_Potter_logo_text_logotype.png"
        alt="Harry Potter logo"
      />
    </a>
    <div id="headers">
      <div>
        <a href="#" @click="charactersSelected()">Characters</a>
      </div>

      <div class="dropdown">
        <button class="dropbtn">House</button>
        <div class="dropdown-content">
          <a href="#" @click="houseSelected('Gryffindor')">Gryffindor</a>
          <a href="#" @click="houseSelected('Ravenclaw')">Ravenclaw</a>
          <a href="#" @click="houseSelected('Slytherin')">Slytherin</a>
          <a href="#" @click="houseSelected('Hufflepuff')">Hufflepuff</a>
        </div>
      </div>
      <div>
        <a href="#" @click="spellsSelected()">Spells</a>
      </div>
    </div>
    <CharactersPage :api-key="apiKey" v-if="showCharacters" />
    <SpellsPage :api-key="apiKey" v-if="showSpells" />
    <!-- the :key attribute is so Vue will watch for changes (select a house then select a different house), so it can rerender the HousePage -->
    <HousePage :api-key="apiKey" :selected-house="selectedHouse" v-if="showHouse" :key="selectedHouse.name" />
  </div>
</template>

<script>
import CharactersPage from "./components/charactersPage";
import SpellsPage from "./components/spellsPage";
import HousePage from "./components/housePage";
import axios from "axios";
import { map, pick, find } from "lodash";

export default {
  name: "App",
  components: {
    CharactersPage,
    SpellsPage,
    HousePage,
  },
  methods: {
    houseSelected(name) {
      this.resetVisibility();
      this.selectedHouse = find(this.houseData, { 'name': name });
      this.showHouse = true;
    },
    charactersSelected() {
      this.resetVisibility();
      this.showCharacters = true;
    },
    spellsSelected() {
      this.resetVisibility();
      this.showSpells = true;
    },
    resetVisibility() {
      this.showHouse = false;
      this.showSpells = false;
      this.showCharacters = false;
    },
  },
  data() {
    return {
      apiKey: "$2a$10$vMB0VNZ9/cIKF4RkUoAKme3vwHer4kinqYPGhSKZnfFq8fN1pg6BC",
      showCharacters: false,
      showSpells: false,
      showHouse: false,
      houseData: [],
      selectedHouse: {},
    };
  },
  mounted() {
    // the house page needs id and name of selected house, so get those ahead of time
    axios
      .get("https://www.potterapi.com/v1/houses?key=" + this.apiKey)
      .then(
        (response) =>
          (this.houseData = map(response.data, (data) =>
            pick(data, ["_id", "name"])
          ))
      );
  },
};
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

#headers  {
  display: flex;
}

#headers > div {
 flex:1;
}

.dropbtn {
  background-color: #b9beb9;
  color: white;
  padding: 16px;
  font-size: 16px;
  border: none;
  cursor: pointer;
}

.dropdown {
  position: static;
  display: block;
} 

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1000;
}

.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
   display:inline-flex;
   width: 95%;
}

.dropdown-content a:hover {
  background-color: #f1f1f1;
  width: 93%;
}

.dropdown:hover .dropdown-content {
  display: block;
}

.dropdown:hover .dropbtn {
  background-color: #727272;
}
</style>
