<template>
  <div id="meus-filmes">
      <h1>Meus Filmes</h1>
      <span v-if="filmes.length < 1">
        Você não possui nenhum filme salvo!
      </span>

      <ul>
        <li v-for="filme in filmes" :key="filme.id" >
          <span>{{filme.nome}}</span>
          <div>
            <router-link tag="button" :to="`/filme/${filme.id}`">Ver detalhes</router-link>
            <button @click="deleteFilme(filme.id)" >Exluir</button>
          </div>
        </li>
      </ul>

  </div>
</template>

<script>
export default {
  data(){
    return{
      filmes: [],
    }
  },
  created(){
    const minhaLista = localStorage.getItem('meuFilme');
    this.filmes = JSON.parse(minhaLista) || [];
  },
  methods:{
    deleteFilme(id){
      let filtroFilmes = this.filmes.filter((filme) => {
        return (filme.id !== id);
      });
      return this.filmes = filtroFilmes;
    }
  },
  watch:{
    filmes(){
      localStorage.setItem('meuFilme', JSON.stringify(this.filmes));
    }
  }
}
</script>

<style scoped>
  #meus-filmes{
    display: flex;
    flex-direction: column;
    width: 100%;
    justify-content: center;
    align-items: center;
  }

  ul{
    padding: 0;
  }

  li{
    padding: 0;
    list-style: none;
    min-width: 600px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  span{
    font-size: 25px;
  }

  button{
    margin-left: 10px;
  }
</style>