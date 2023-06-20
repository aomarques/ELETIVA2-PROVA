<template>
  <div class="page">
    <div class="buscar">
      <img alt="Pokemon" src="https://user-images.githubusercontent.com/29473781/180619084-a56960ab-7efa-4e34-9d33-4e3e581d62ff.png" class="disney-img">            
      <input type="text" v-model="searchTerm" placeholder="Digite o nome do Pokémon" />
      <button @click="searchPokemon">PESQUISAR</button>

      <div v-if="isLoading">
        Carregando...
      </div>

      <div v-else-if="imageUrl">
        <img :src="imageUrl" alt="Pokemon" />
      </div>

      <div v-else>
        Nenhum Pokémon encontrado.
      </div>
    </div>
  </div>
</template>

<script>
import getPokemonImage from '../services/api.js';

export default {
  data() {
    return {
      searchTerm: '',
      imageUrl: '',
      isLoading: false,
    };
  },
  methods: {
    async searchPokemon() {
      if (this.searchTerm.trim() === '') {
        return;
      }

      this.isLoading = true;

      try {
        this.imageUrl = await getPokemonImage(this.searchTerm.toLowerCase());
      } catch (error) {
        console.error(error);
        this.imageUrl = '';
      }

      this.isLoading = false;
    },
  },
  
};

</script>

<style scoped>
  .buscar {
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        top: 50px;
        color: #fff;
        width: 100%;
        margin-bottom: 50px;
        justify-content: center;
        align-items: center;
    }
    .buscar input {
        border: 5px solid #fff;
        border-radius: 5px;
        height: 25px;
        padding-left: 10px;        
        color: darkgray;
        width: 60%;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        font-size: 20px;
        align-items: center;
    }
    .buscar button{
      border-radius: 10px;
      background-color: white;
      margin-top: 20px;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      font-size: 20px;
      align-items: center;
      padding: 20px;
    }
    .page{
        position: absolute;
        display: flex;
        flex-direction: column;
        min-height: 100%;
        min-width: 100%;        
        align-items: center;
        background: rgb(196, 77, 77);     
    }
    .buscar button:hover{
      background-color: #4CAF50; 
      color: white;
    }

</style>
