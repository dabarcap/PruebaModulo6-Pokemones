<script>
export default { 
    name: 'PokemonCard', 
    props: ['pokemon'], 
    data() { 
        return { 
            userGuess: '', // Input del usuario para adivinar el nombre 
            isRevealed: false // Estado de si el Pokémon ha sido descubierto 
        }; 
    }, 
    methods: { // Método para verificar si la adivinanza es correcta 
        checkGuess() { 
            if (this.userGuess.toLowerCase() === this.pokemon.name.toLowerCase()) { 
                this.isRevealed = true; 
                this.$emit('discovered'); // Emitir un evento para notificar al componente padre 
            } else { 
                alert('Nombre incorrecto. ¡Intenta de nuevo!'); 
            } 
        } 
    } 
}; 
</script>

<template>
    <div class="pokemon-card"> <!-- Imagen del Pokémon con filtro aplicado inicialmente --> <img :src="pokemon.image"
            :class="{ revealed: isRevealed }" /> <!-- Input y botón para adivinar el nombre del Pokémon -->
        <div v-if="!isRevealed"> <input v-model="userGuess" @keyup.enter="checkGuess"
                placeholder="Adivina el Pokémon" /> <button @click="checkGuess">Descubrir</button> </div>
        <!-- Nombre del Pokémon descubierto -->
        <p v-else>{{ pokemon.name }}</p>
    </div>
</template>

<style scoped>
/* Estilos del componente PokemonCard */
.pokemon-card {
    text-align: center;
    padding: 10px;
    border: 1px solid #dddddd;
    border-radius: 5px;
    background-color: #ffffff;
    box-shadow: 0 0 10px #0000001a;
}

.pokemon-card img {
    width: 100px;
    height: 100px;
    filter: brightness(0); /* Aplicar filtro a la imagen */
    transition: filter 0.3s; 
}

.pokemon-card img.revealed { 
    filter: none; /* Remover filtro cuando el Pokémon es descubierto */
} 

.pokemon-card input {
    margin-top: 10px;
    padding: 5px;
    border: 1px solid #dddddd;
    border-radius: 5px;
}

.pokemon-card button {
    margin-top: 5px;
    padding: 5px 10px;
    border: none;
    border-radius: 5px;
    background-color: #007bff;
    color: #ffffff;
    cursor: pointer;
    transition: background-color 0.3s;
}

.pokemon-card button:hover {
    background-color: #0056b3;
}
</style>
