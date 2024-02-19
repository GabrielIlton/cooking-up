<script lang="ts">
import SelectIngredient from './SelectIngredient.vue';
import ShowRecipe from './ShowRecipe.vue';
import YourList from './YourList.vue';
import Tag from './Tag.vue';

type Page = 'SelectIngredient' | 'ShowRecipe'

export default {
  data() {
    return {
      ingredientes: [] as string[],
      content: 'SelectIngredient' as Page
    };
  },
  components: { SelectIngredient, Tag, YourList, ShowRecipe },
  methods: {
    addIngredient(ingredient: string) {
      this.ingredientes.push(ingredient)
    },
    removeIngredient(ingredient: string) {
      const ingredientToRemove = this.ingredientes.indexOf(ingredient)

      this.ingredientes.splice(ingredientToRemove, 1)
    },
    navigate(page: Page) {
      // if (page === 'SelectIngredient') this.ingredientes.length = 0
      this.content = page
    }
  }
}
</script>

<template>
  <main class="conteudo-principal">
    <YourList v-if="content === 'SelectIngredient'" :listIngredients="ingredientes"
      @removeIngredient="removeIngredient($event)" />

    <KeepAlive include="SelectIngredient">
      <SelectIngredient v-if="content === 'SelectIngredient'" @addIngredient="addIngredient($event)"
        @removeIngredient="removeIngredient($event)" @showRecipe="navigate('ShowRecipe')" />

      <ShowRecipe v-else-if="content === 'ShowRecipe'" @editRecipe="navigate('SelectIngredient')"
        :ingredientsToFind="ingredientes" />
    </KeepAlive>
  </main>
</template>

<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 3.75rem 3.75rem;
  background: var(--creme, #FFFAF3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>