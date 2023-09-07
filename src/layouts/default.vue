<template>
	<Navigation />
	<div class="flex flex-col items-center justify-center">
		<router-view v-slot="{ Component }">
			<transition name="fade" mode="out-in">
				<component :is="Component" />
			</transition>
		</router-view>
	</div>
	<Footer />
</template>

<script setup></script>
<style scoped lang="scss"></style>
