<template>
  <div class="hello">
    <h1> Characters </h1>
  <table v-if="characters.length > 0" id="characters">
    <tr>
      <th v-for="header in tableHeaders" :key="header">{{header}}</th>
    <tr>

    <tr v-for="character in characters" :key="character.name"> 
      <td>{{character.name}}</td>
      <td>{{character.house ? character.house: 'None'}}</td>
      <td>{{character.patronus ? character.patronus : 'None'}}</td>
      <td>{{character.species}}</td>
      <td>{{character.bloodStatus}}</td>
      <td>{{character.role}}</td>
      <td>{{character.school ? character.school : 'None'}}</td>
      <td>{{character.deathEater ? 'Yes' : 'No'}}</td>
      <td>{{character.dumbledoresArmy ? 'Yes' : 'No'}}</td>
      <td>{{character.orderOfThePhoenix ? 'Yes' : 'No'}}</td>
      <td>{{character.ministryOfMagic? 'Yes' : 'No'}}</td>
      <td>{{character.alias}}</td>
      <!-- this only exists if wand is set. not cool -->
      <td>{{character.wand}}</td>
      <td>{{character.boggart}}</td>
      <td>{{character.animagus}}</td>

  </tr>

  </table>
  <h2 class="error" v-else>There was a problem retreiving the characters</h2>
  </div>
</template>
<script>
import axios from 'axios';
// import {omit, mapKeys} from 'lodash';
export default {
  name: 'CharacterPage',
 data () {
   return {
   apiKey :'$2a$10$vMB0VNZ9/cIKF4RkUoAKme3vwHer4kinqYPGhSKZnfFq8fN1pg6BC',
   characters:[],
   tableHeaders:[
    'Name',
    'House',
    'Patronus',
    'Species',
    'Blood Status',
    'Role',
    'School',
    'Death Eater?',
    `Dumbledore's Army?`,
    'Order Of The Phoenix?',
    'Ministry Of Magic?',
    'Alias',
    'Wand',
    'Boggart',
    'Animagus',
   ]
   }
 },
 mounted (){
   axios
   .get('https://www.potterapi.com/v1/characters?key=' + this.apiKey)
   .then(response => this.characters = response.data);
 },
//  computed: {
//     getTableHeaders () {
//       let characterWithWand = this.characters.find(character => character.wand);
//       return mapKeys(omit(characterWithWand, ['_id', '__v']), (_, key) =>{
//         return key.to
//       })
//   },
//  }
}
</script>

<style scoped>

#characters {
  font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  max-width: 100%;
}

#characters td, #customers th {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

#characters tr:nth-child(even){background-color: #f2f2f2;}

#characters tr:hover {background-color: #ddd;}

#characters th {
  padding-top: 12px;
  padding-bottom: 12px;
  background-color: #4CAF50;
  color: white;
}
</style>
