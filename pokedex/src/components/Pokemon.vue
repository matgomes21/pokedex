<template>
    <div class="container">
        <img :src="pokemon.front" />
        <h1>{{id}} {{name | upper}}</h1>
        <p>{{pokemon.type}}</p>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    created: function() {
        axios.get(this.url).then(data => {
            this.pokemon.type = data.data.types[0].type.name;
            this.pokemon.front = data.data.sprites.front_default;
            this.pokemon.back = data.data.sprites.back_default;
        });
    },
    data() {
        return {
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    props: {
        id: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function(name){
            var filteredName = name[0].toUpperCase() + name.slice(1);
            return filteredName;
        }
    }    
}
</script>

<style scoped>
    .container {
        justify-content: center;
        align-items: center;
        margin-bottom: 2%;
        box-shadow: 0px 4px 4px rgba(0,0,0,0.25);
        width: 40%;
    }
</style>