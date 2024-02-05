<script lang="ts">
import Tag from './Tag.vue';

export default {
	components: { Tag },
	props: {
		ingrediente: { type: String, required: true }
	},
	data() {
		return { selecionado: false }
	}
}
</script>

<template>
	<button class="ingrediente" @click="selecionado = !selecionado" :aria-pressed="selecionado">
		<Tag :texto="ingrediente" :is_active="selecionado" />
	</button>
</template>

<style scoped>
.ingrediente {
	cursor: pointer;
}
</style>