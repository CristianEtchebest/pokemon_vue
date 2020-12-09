
<template>   
    <form action="">                      
        <div class="form-group row ">
            <label for="" class="col-sm-3 col-form-label" >Escolha o Pokemon:</label>
            <div class="col-sm-5">
                <select name="listPoke" id="listPoke" class="form-control col-sm-7 opt" v-model="pokeList" >
                    <option v-for="pokemon in pokemons" :value='pokemon.url' :key="pokemon.name"  >
                        <span>{{ pokemon.name }}</span>
                    </option>
                </select>
            </div>
            <div class="col-sm-4">
                <button class="btn btn-primary" type="submit" v-on:click.prevent="addDados">Visualizar dados</button>
            </div> 
        </div>                
    </form>    
</template>

<script>
import axios from 'axios'
export default {    
    data(){
        return{            
            pokemons:"",
            pokeList:""
        }
    },
    mounted(){   
        this.getTodos(); 
    },

    methods:{
        addDados(){
            this.$emit('select', {
                selectPok: this.pokeList
            });
        },
        // Pega a URL para listar os pokemons
        getTodos(){      
            axios
            .get("http://127.0.0.1:8000/api/listar/")
            .then(response => {this.pokemons = response.data});            
        }
    }  
}
</script>
<style scoped>
    .content{width: 70%; margin: 0 auto;font-size: 1.2em;padding: 10px;}
    .opt{font-size: 1.2em;}
    .btn{border: 0;}
</style>