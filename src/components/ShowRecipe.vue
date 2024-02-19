<script lang="ts">
import type IRecipe from '../interfaces/IRecipe';
import CardRecipe from './CardRecipe.vue';
import MainButton from './MainButton.vue';
import { getRecipes } from '../http';
import { PropType } from 'vue';

export default {
  data() {
    return {
      recipes: [] as IRecipe[]
    }
  },
  props: {
    ingredientsToFind: { type: Array as PropType<string[]>, required: true }
  },
  async created() {
    this.recipes = await getRecipes()

    this.recipes = this.recipes.filter(recipe => recipe.ingredientes.every(ingredient => this.ingredientsToFind.includes(ingredient)))
  },
  components: { CardRecipe, MainButton },
  emits: ['editRecipe']
}
</script>

<template>
  <section class="mostrar-recipe">
    <h1 class="cabecalho titulo-recipe">
      Receitas
    </h1>

    <p class="paragrafo-lg resultados-encontrados">
      Resultados encontrados: {{ recipes.length }}
    </p>

    <div v-if="recipes.length" class="recipes-wrapper">
      <p class="paragrafo-lg informacoes">
        Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!
      </p>

      <ul class="recipes">
        <li v-for="recipe of recipes">
          <CardRecipe :recipe="recipe" />
        </li>
      </ul>
    </div>

    <div v-else class="recipes-nao-encontradas">
      <p class="paragrafo-lg recipes-nao-encontradas__info">
        Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?
      </p>

      <img src="../assets/images/sem-receitas.png"
        alt="Desenho de um ovo quebrado. A gema tem um rosto com uma expressão triste.">
    </div>

    <MainButton texto="Editar lista!" @click="$emit('editRecipe')" />
  </section>
</template>

<style scoped>
.mostrar-recipe {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.titulo-recipe {
  color: var(--verde-medio, #3D6D4A);
  margin-bottom: 1.5rem;
}

.resultados-encontrados {
  color: var(--verde-medio, #3D6D4A);
  margin-bottom: 0.5rem;
}

.recipes-wrapper {
  margin-bottom: 3.5rem;
}

.informacoes {
  margin-bottom: 2rem;
}

.recipes {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.recipes-nao-encontradas {
  margin-bottom: 2rem;
}

.recipes-nao-encontradas__info {
  margin-bottom: 0.5rem;
}

@media only screen and (max-width: 767px) {
  .recipe-wrapper {
    margin-bottom: 2rem;
  }
}
</style>