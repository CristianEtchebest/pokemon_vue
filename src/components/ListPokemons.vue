<template>
    <div class="container">
        <h1>{{name}}</h1>
        <form action="">                      
                <div class="form-group row ">
                    <label for="" class="col-sm-3 col-form-label" >Escolha o Pokemon:</label>
                    <div class="col-sm-5">
                        <select name="listPoke" id="listPoke" class="form-control col-sm-7" v-model="pokeList" >
                            <option v-for="pokemon in pokemons" :value='pokemon.url' :key="pokemon.name" > {{ pokemon.name }}</option>
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
            <p>Nome: {{pokeDados.name}}</p>
            <p>Altura: {{pokeDados.height}}</p>
            <p>Peso: {{pokeDados.weight}}</p> 
            <p>Habilidade: </p>
            <p>Velocidade: </p>
            <p>Defesa: </p>
            <p>Ataque: </p>
            <p>Hp: </p>
            <p>Total: </p>
            <h3>Evoluções</h3>
            <p>
                <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/2.png"  alt="" /> >> 
                <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/2.png" alt="" /> >>
                <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/3.png" alt="" /> 
            </p>

        </div>
    </div>
</template> 


<script>
import axios from 'axios'
export default { 
    data(){
        return {
            namei: 'Lista de Pokemons',    
            pokemons:null,
            pokeDados:""        
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
            axios.get(this.pokeList).then(response => this.pokeDados = response.data) 
        }
    }

}
</script>
