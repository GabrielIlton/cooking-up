import Banner from './components/Banner.vue';
<script lang="ts">
import MainContent from './components/MainContent.vue';
import Banner from './components/Banner.vue';
import Foot from './components/Foot.vue';

export default { components: { Banner, MainContent, Foot } }
</script>

<template>
	<Banner />
	<MainContent />
	<Foot />
</template>

<style></style>