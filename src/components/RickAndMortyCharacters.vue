<template>
    <div>
      <h1>Personajes de Rick y Morty</h1>
      <!-- <ul>
        <li v-for="character in characters" :key="character.id">
          {{ character.name }} - {{ character.species }} - {{ character.status }} -   <img :src="character.image" />
          <button @click="getCharacterDetails(character.id)">Ver detalles</button>
        </li>
      </ul> -->
      <div v-if="selectedCharacter">
        <h2>{{ selectedCharacter.name }}</h2>
        <p>{{ selectedCharacter.status }} - {{ selectedCharacter.species }}</p>
        <p>{{ selectedCharacter.origin.name }} - {{ selectedCharacter.location.name }}</p>
        <img :src="selectedCharacter.image" :alt="selectedCharacter.name" />
      </div>
    </div>


    <link href="https://fonts.googleapis.com/css?family=Montserrat:400,700" rel="stylesheet">

<section class="hero-section">
  <div class="card-grid">
    <div v-for="character in characters" :key="character.id" class="card">
      <a href="" class="card" v-if="selectedCharacter"></a>  
      <div  class="card__background"><img :src="character.image" /></div>
      <div class="card__content">
        <p class="card__category">{{ character.species }}</p>
        <h3 class="card__heading">{{ character.name }}</h3>
        <button @click="getCharacterDetails(character.id)" class="button">Ver detalles</button>  
      </div>
      
    </div>
</div>
</section>


  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        characters: [],
        selectedCharacter: null,
      };
    },
    mounted() {
      axios
        .get('https://rickandmortyapi.com/api/character')
        .then(response => {
          this.characters = response.data.results;
        })
        .catch(error => {
          console.error(error);
        });
    },
    methods: {
      getCharacterDetails(id) {
        axios
          .get(`https://rickandmortyapi.com/api/character/${id}`)
          .then(response => {
            this.selectedCharacter = response.data;
          })
          .catch(error => {
            console.error(error);
          });
      },
    },
  };
  </script>


<style>



:root{
    --background-dark: #2d3548;
    --text-light: rgba(255,255,255,0.6);
    --text-lighter: rgba(255,255,255,0.9);
    --spacing-s: 8px;
    --spacing-m: 16px;
    --spacing-l: 24px;
    --spacing-xl: 32px;
    --spacing-xxl: 64px;
    --width-container: 1200px;
  }
  
  *{
    border: 0;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  html{
    height: 100%;
    font-family: 'Montserrat', sans-serif;
    font-size: 14px;
  }
  
  body{
    height: 100%;
  }

  h1{
    text-align: center;
    padding: 2%;
    background-image: linear-gradient(15deg, #0f4667 0%, #2a6973 150%);;
  }
  
  .hero-section{
    align-items: flex-start;
    background-image: linear-gradient(15deg, #0f4667 0%, #2a6973 150%);
    display: flex;
    min-height: 100%;
    justify-content: center;
    padding: var(--spacing-xxl) var(--spacing-l);
  }
  
  .card-grid{
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    grid-column-gap: var(--spacing-l);
    grid-row-gap: var(--spacing-l);
    max-width: var(--width-container);
    width: 100%;
  }
  
  @media(min-width: 540px){
    .card-grid{
      grid-template-columns: repeat(2, 1fr); 
    }
  }
  
  @media(min-width: 960px){
    .card-grid{
      grid-template-columns: repeat(4, 1fr); 
    }
  }
  
  .card{
    list-style: none;
    position: relative;
  }
  
  .card:before{
    content: '';
    display: block;
    padding-bottom: 150%;
    width: 100%;
  }
  
  .card__background{
    background-size: cover;
    background-position: center;
    border-radius: var(--spacing-l);
    bottom: 0;
    filter: brightness(0.75) saturate(1.2) contrast(0.85);
    left: 0;
    position: absolute;
    right: 0;
    top: 0;
    transform-origin: center;
    transform: scale(1) translateZ(0);
    transition: 
      filter 200ms linear,
      transform 200ms linear;
  }
  
  .card:hover .card__background{
    transform: scale(1.05) translateZ(0);
  }
  
  .card-grid:hover > .card:not(:hover) .card__background{
    filter: brightness(0.5) saturate(0) contrast(1.2) blur(20px);
  }
  
  .card__content{
    left: 0;
    padding: var(--spacing-l);
    position: absolute;
    top: 0;
  }
  
  .card__category{
    color: var(--text-light);
    font-size: 0.9rem;
    margin-bottom: var(--spacing-s);
    text-transform: uppercase;
  }
  
  .card__heading{
    color: var(--text-lighter);
    font-size: 1.9rem;
    text-shadow: 2px 2px 20px rgba(0,0,0,0.2);
    line-height: 1.4;
    word-spacing: 100vw;
  }

  .button{
    background: transparent;
    color: white;
    font-size: 1rem;
    text-align: right;
  }

</style>
  