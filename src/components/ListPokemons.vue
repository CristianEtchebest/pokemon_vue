<template>
    <div class="container">
         <h1>{{nome}}</h1>
        <SearchPokemons v-on:select="addDados"></SearchPokemons>
        <hr>
        <div class="content">
            <h3 >Dados do Pokemon</h3>
            <div class="info">
                <p><b>Nome:</b> {{pokeDados.name}}</p>
                <p><b>Altura:</b> {{pokeDados.height}}</p>
                <p><b>Peso:</b> {{pokeDados.weight}}</p>
                <p><b>Velocidade:</b>{{speed}}</p>
                <p><b>Defesa:</b> {{defense}}</p>
                <p><b>Defesa Especial:</b> {{specialDefense}}</p>
                <p><b>Ataque:</b>{{attack}}</p>
                <p><b>Ataque Especial:</b> {{specialAttack}}</p>
                <p><b>HP:</b> {{hp.base_stat}}</p> 
            </div>
            <div class="img-pok">
                <h3>Imagem Pokemon</h3>
                <img :src="image.front_default" :alt="pokeDados.name" :title="pokeDados.name" />                    
            </div>          
        </div>
    </div>
</template>
<script>
import SearchPokemons from './SearchPokemons'
import axios from 'axios'
export default {
    components:{
        SearchPokemons
    },

    data(){
        return {         
            pokeDados:'',
            nome: 'Lista de Pokemons', 
            hp:'',
            attack:'',
            defense:'',
            specialAttack:'',
            specialDefense:'',
            speed:'',
            image:''
        }  
    },
    methods: {    
        //Exibe o array na variavel pokeDados para ser exibida no campos de informações do pokemon
        addDados(selecao){
            axios.get(selecao.selectPok).then(response => {[
                this.pokeDados = response.data,                
                this.hp=response.data.stats[0],
                this.attack=response.data.stats[1].base_stat,
                this.defense=response.data.stats[2].base_stat,
                this.specialAttack=response.data.stats[3].base_stat,
                this.specialDefense=response.data.stats[4].base_stat,
                this.speed=response.data.stats[5].base_stat,
                //exibe imagem
                this.image=response.data.sprites,

            ]});           
        }
    },    
}
</script>

<style>
body{
    background-color: #fefefe;
}
.container{
    width:60%; 
}
.content{
    width: 100%;
    float: left;
    padding: 10px;
    border-radius: 8px;
   box-shadow: 0 5px 5px 5px rgba(0, 0, 0, 0.2);
   background-color: white;
}
.info{
    width:50%;
    float: left;
    font-size: 1.2em;
}
.img-pok{
    width: 50%;
    float: right;
}
.img-pok img{
    width: 200px;
}
@media only screen and (max-width: 920px){
transition: all 0.3s;
    .img-pok{
        width: 100%;
        text-align: center;
    }
    .info{
        width:100%;
        font-size: 1.2em;
        text-align: center;
    }
    .content h3{
        text-align: center;
    } 
}
</style>
