<template>
    <div class="container">
        <h1>{{nome}}</h1>
        <form action="">                      
                <div class="form-group row ">
                    <label for="" class="col-sm-3 col-form-label" >Escolha o Pokemon:</label>
                    <div class="col-sm-5">
                        <select name="listPoke" id="listPoke" class="form-control col-sm-7 opt" v-model="pokeList" >
                            <option v-for="pokemon in pokemons" :value='pokemon.url' :key="pokemon.name"  ><span>{{ pokemon.name }}</span></option>
                        </select>
                    </div>
                    <div class="col-sm-4">
                        <button class="btn btn-primary" type="submit"   v-on:click.prevent="addDados">Ver daddos</button>
                    </div> 
                </div>                
        </form>
        <hr>            
        <div class="content ">
            <h3 >Dados do Pokemon</h3>
            <ul class="list-group">
                <li class="list-group-item"><b>Nome:</b> {{pokeDados.name}}</li>
                <li class="list-group-item"><b>NAltura:</b> {{pokeDados.height}}</li>
                <li class="list-group-item"><b>Peso:</b> {{pokeDados.weight}}</li>
                <li class="list-group-item"><b>Velocidade:</b>{{speed}}</li>
                <li class="list-group-item"><b>Defesa:</b> {{defense}}</li>
                <li class="list-group-item"><b>Defesa Especial:</b> {{specialDefense}}</li>
                <li class="list-group-item"><b>Ataque:</b>{{attack}}</li>
                <li class="list-group-item"><b>Ataque Especial:</b> {{specialAttack}}</li>
                <li class="list-group-item"><b>HP:</b> {{hp}}</li>
                <li class="list-group-item"><h3>Pokemon:</h3> <img :src="image.front_default" :alt="pokeDados.name" :title="pokeDados.name" class="img-pok img" /></li>
            </ul> 
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default { 
    data(){
        return {
            nome: 'Lista de Pokemons',    
            pokemons:null,
            pokeDados:"",
            pokeList:"",
            
            hp:'',
            attack:'',
            defense:'',
            specialAttack:'',
            specialDefense:'',
            speed:'',
            image:''
        } 
    },
    mounted(){   
        this.getTodos();   
    },
    methods: {
        // Pega a URL para listar os pokemons
        getTodos(){
            axios
            .get("http://localhost:8000/api/listar/")
            .then( response => (this.pokemons = response.data))       
        },        
        //Exibe o array na variavel pokeDados para ser exibida no campos de informações do pokemon
        addDados(){
            axios.get(this.pokeList).then(response => {[
                this.pokeDados = response.data,
                this.hp=response.data.stats[0].base_stat,
                this.attack=response.data.stats[1].base_stat,
                this.defense=response.data.stats[2].base_stat,
                this.specialAttack=response.data.stats[3].base_stat,
                this.specialDefense=response.data.stats[4].base_stat,
                this.speed=response.data.stats[5].base_stat,
                //exibe imagem
                this.image=response.data.sprites
            ]});           
        }
    }
}
</script>

<style>
   

.img-pok{
    width: 200px;
}
.content{
    width: 70%;
    margin: 0 auto;
    font-size: 1.2em;
}
.opt{
    font-size: 1.2em;
}
</style>
