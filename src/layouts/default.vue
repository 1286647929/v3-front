<template>
	<Navigation />
	<div class="flex flex-col items-center justify-center">
		<router-view v-slot="{ Component }">
			<transition name="fade" mode="out-in">
				<component :is="Component" @handleChange="callback" />
			</transition>
		</router-view>
	</div>
	<Footer v-if="footVisible" />
</template>

<script setup>
const footVisible = ref(true)

const callback = (value) => {
	footVisible.value = value
	console.log(value)
}
</script>
<style scoped lang="scss"></style>
