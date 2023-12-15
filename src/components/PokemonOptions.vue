
<template>
<div >
  <h3>Pokemon Options</h3>
  <b>{{ countScore }}</b>
  <div class="options-container">
    <ul>
      <li v-for="pokemon in pokemons" :key="pokemon.id" @click="$emit('selection',pokemon.id)">{{pokemon.name}}</li>
    </ul>
  </div>
</div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
    count: {
      type: Number,
      default: 0,
      required:false
    }
  },
  methods: {
    hola() {
      
    }
  }
  
}
</script>
<style scope>
/* Pokemon Options */
ul {
    list-style-type: none;
}
li {
    background-color: rgba(251, 251, 251, 0.834);
    border-radius: 5px;
    border: 1px solid rgba(2, 2, 2, 0.274);
    cursor: pointer;
    margin-bottom: 10px;
    width: 270px;
}

li:hover {
    background-color: rgba(54, 52, 52, 0.453);
}

.options-container {
    display: flex;
    justify-content: center;
}
</style>