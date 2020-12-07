<template>
    <div class="container">
        <h1>{{name}}</h1>
        <form action="">                      
                <div class="form-group row ">
                    <label for="" class="col-sm-3 col-form-label" >Escolha o Pokemon:</label>
                    <div class="col-sm-9">
                        <!--select name="listPoke" id="listPoke" class="form-control col-sm-7" >
                            <option v-for="todo in todos" :value='todo.count' :key="todo.name" >{{ todo.name }}</option>
                        </select-->
                    </div>
                    
                </div>                
        </form>
        <hr>
        <table>
            <tbody>
                <p>{{todos}}</p>
            <tr v-for="todo in todos" :key="todo">
            <td>{{todo.name}}</td>
            </tr>

            </tbody>
            </table>    
            
        <div class="content ">
            <h3>Dados do Pokemon</h3>
            <p>Nome: </p>
            <p>Habilidade: </p>
            <p>Velocidade: </p>
            <p>Defesa: </p>
            <p>Ataque: </p>
            <p>Hp: </p>
            <p>Total: </p>
            <h3>Evoluções</h3>
            <p>
                <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png" alt="" /> >> 
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
         /*name: 'Lista de Pokemons',
         poke: null,         
         litasPokemons: [],*/
         todos:[]
        }
    },
    mounted(){
        //this.listarDados();      
        this.getTodos();
    },

    methods: {
        getTodos(){
            axios
            .get('http://pokeapi.co/api/v2/pokemon/')
            .then( Response => {this.todos = Response.data })
            .catch(e => console.log(e))
        }        
    }    

}
</script>
