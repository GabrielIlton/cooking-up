<script lang="ts">
import { PropType } from 'vue';
import IRecipe from '../interfaces/IRecipe';

export default {
	props: {
		recipe: { type: Object as PropType<IRecipe>, required: true }
	}
}
</script>

<template>
	<article class="recipe">
		<header class="recipe__cabecalho">
			<img :src="`/imagens/receitas/${recipe.imagem}`" alt="" class="recipe__imagem">
		</header>

		<section class="recipe__corpo">
			<h2 class="paragrafo recipe__nome"> {{ recipe.nome }} </h2>
		</section>
	</article>
</template>

<style scoped>
.recipe {
	display: flex;
	width: 17.625rem;
	max-width: 19.5rem;
	flex-direction: column;
	align-items: center;

	border-radius: 1rem;
	background: var(--Branco, #FFF);
	box-shadow: 4px 4px 12px 0px rgba(68, 68, 68, 0.08);
}

.recipe__corpo {
	padding: 2rem 1rem;
}

.recipe__imagem {
	width: 100%;
	border-radius: 1rem 1rem 0rem 0rem;
	display: block;
}

.recipe__nome {
	font-weight: 700;
	color: var(--cinza, #444);
}
</style>