<script lang="ts">
import type ICategorie from '../interfaces/ICategorie';
import CardCategorie from './CardCategorie.vue';
import MainButton from './MainButton.vue';
import { getCategories } from '../http';

export default {
  name: 'SelectIngredient',
  data() {
    return {
      categorias: [] as ICategorie[]
    }
  },

  async created() {
    this.categorias = await getCategories()
  },
  components: { CardCategorie, MainButton },
  emits: ['addIngredient', 'removeIngredient', 'showRecipe']
}
</script>

<template>
  <section class="selecionar-ingredientes">
    <h1 class="cabecalho titulo-ingredientes">
      Ingredientes
    </h1>

    <p class="paragrafo-lg instrucoes">
      Selecione abaixo os ingredientes que você deseja usar nessa receita!
    </p>

    <ul class="categorias">
      <li v-for="categoria in categorias">
        <CardCategorie :categoria="categoria" @addIngredient="$emit('addIngredient', $event)"
          @removeIngredient="$emit('removeIngredient', $event)" />
      </li>
    </ul>

    <p class="paragrafo dica">
      *Atenção: consideramos que você tenha em casa sal, pimenta e água.
    </p>

    <MainButton texto="Buscar receitas!" @click="$emit('showRecipe')" />
  </section>
</template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}
</style>