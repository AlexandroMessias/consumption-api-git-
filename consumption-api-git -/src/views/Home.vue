<template>
  <div class="central">
  <section class="secao"><!-- Padrão de código BEM(Block.Element.Modifier), seria legal pesquisar -->
  <header class="secao__header">
      <section class="banner">
        <h1>GITHUB API</h1>
        <h2>Show GitHub users</h2>
      </section>
    </header>
    <main v-if='nome!= null' class="item secao__main">
        <div class="itens nome">
            <img src="../assets/name.png" alt="nameimg" width=60 height=40>
            <p>NOME</p>
            {{nome}}
        </div> 
        <div class="itens login">
            <img src="../assets/login.png"  alt="loginimg" width=60 height=40>
            <p>LOGIN</p>
            {{login}}
        </div>
        <div class="itens repositorio">
            <img src="../assets/repositorio.png" alt="repositorioimg" width=60 height=40>
            <p>REPOSITÓRIOS PÚBLICOS</p>
            {{repositorio}} repositórios
        </div>

        <div class="itens seguidores">
            <img src="../assets/seguidores.png" alt="seguidoresimg" width=60 height=40>
            <p>SEGUITORES</p>
            {{seguidores}} seguidores
        </div>
        <div class="itens empresa">
            <img src="../assets/empresa.png" alt="empresaimg" width=60 height=40>
            <p>EMRPESA</p>
            {{empresa}}
        </div>
        <div class="itens site">
            <img src="../assets/site.png" alt="some text" width=60 height=40>
            <p>SITE</p>
            <a :href="site">{{site}}</a>
        </div>

        <div class="avatar">
            <div class="infoavatar">
                <img :src="avatar" alt="some text">
                <p class="nomeavatar">{{nome}}</p>
                <p class="loginavatar">{{login}}</p>
            </div>
        </div>

        <div class="itens bio">
            <div>
                <p class="infobio">{{bio}}</p>
            </div>
        </div> 
    </main>
    <div v-else class="erro"><h1>USUARIO NÃO ENCONTRADO</h1></div>
    <footer class="secao__footer">
        <div class="gitimg">
            <div>
                <img src="../assets/GitHub.png" alt="some text" width=60 height=40>
            </div>
        </div>
        <div class="teste">
            <p class = "textfooter">O Github API Crawler serve para procurar por desenvolvedores por meio da API do Github</p>
            <p class = "textfooter2">PENSANDO COM CARINHO POR LUCCAS PIOLA</p>
        </div>
    </footer>
  </section>
  </div>

</template>

<script>
import axios from 'axios';

//** Digitar o URL do Usuario do git por exemplo 'diego3g' */
var usuario = 'diego3g';

export default {
    name: 'home',
    data () {
    return {
      nome: null,
      login: 'Vazio',
      repositorio: 0,
      seguidores: 0,
      empresa: 'Vazio',
      site: 'Nenhum Site Disponivel',
      avatar: 0,
      bio: 'Nenhuma biografia encontrada',
    }
  },
  mounted () {
    axios
      .get(`https://api.github.com/users/${usuario}`)
      .then(response => (this.nome = response.data.name) +
      (this.login = response.data.login) + 
      (this.repositorio = response.data.public_repos)+
      (this.seguidores = response.data.followers)+
      (this.empresa = response.data.company)+
      (this.site = response.data.blog)+
      (this.avatar = response.data.avatar_url)+
      (this.bio = response.data.bio)
      )
  },
    
}
</script>

<style>
  @import '../components/stylehome.css';

  @media (max-width: 890px){
        .secao__main {

            display: flex;
            flex-direction: column;
            width: 100%;
        }

        footer{
            display: flex;
            flex-wrap: wrap;
            flex-direction: row;
            width: 100%;
       
        }   
        .gitimg img{
        display: none; 
    }
    }
    
</style>