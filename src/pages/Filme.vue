<template>
  <div id="filme">
      <div class="container">
        <h2>{{filme.nome}}</h2>
        <img :src="filme.foto" alt="">
        <h3>Sinopse</h3>
        <p>{{filme.sinopse}}</p>
        <div class="botoes">
          <router-link tag="button" to="/" >Ver mais filmes</router-link> 
          <button @click="salvarFilme">Salvar</button>
          <button>
            <a :href="`https://www.youtube.com/results?search_query=${filme.nome}`" target="blank">
              Trailer
            </a>
          </button>
        </div>
      </div>
  </div>
</template>

<script>

import api from '../service/api';
export default {
  props:['id'],
  data(){
    return{
      filme: {}      
    }
  },
  async created(){
    const response = await api.get(`?api=filmes/${this.id}`);
    this.filme = response.data;
  },
  methods:{
    salvarFilme(){
      const listaFilmes = localStorage.getItem('meuFilme');

      let filmes = JSON.parse(listaFilmes) || [];

      const hasFilme = filmes.some((filme) => filme.id === this.filme.id);

      if(hasFilme){      
        alert('Este filme já está salvo!')
        return;
      }
        filmes.push(this.filme);
        localStorage.setItem('meuFilme', JSON.stringify(filmes));        
        alert('Filme salvo com sucesso!');      
    }
  }
}
</script>

<style scoped>
.container{
        display: flex;
        justify-content: center;
        flex-direction: column;
        max-width: 900px;
    }

    h2{
      color: #FFF;
      margin-bottom: 0px;
      background: brown;
      padding: 15px;
      border-top-left-radius: 20px;
      border-top-right-radius: 20px;
    }

    .container img{
        width: 100%;
        border-bottom-left-radius: 20px;
        border-bottom-right-radius: 20px;
    }

    button{
      margin-right: 5px;
      border-radius: 5px;
      margin-top: 15px;
      cursor: pointer;
      border:0;
      padding: 12px;
      font-size: 20px;
      transition: all 0.5s;
      outline: none;
    }
    button:hover{
      background: brown;
      color: #FFF;
    }

    a{
      text-decoration: none;
      color: #000;
      transition: all 0.5s;
    }

    a:hover{
      color: #FFF;
    }
</style>

