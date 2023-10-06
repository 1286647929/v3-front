<template>
	<Navigation v-if="Visible" />
	<div class="flex flex-col items-center justify-center">
		<router-view v-slot="{ Component }">
			<transition name="fade" mode="out-in">
				<component :is="Component" @handleChange="callback" />
			</transition>
		</router-view>
	</div>
	<Footer v-if="Visible" />
</template>

<script setup>
const route = useRoute()
const Visible = ref(true)

const callback = (value) => {
	Visible.value = value
	// console.log(value)
}

/**
 * 监听路由导航栏的变化
 */
watch(
	() => route.path,
	async (path) => {
		if (path === '/') {
			Visible.value = true
		}
	},
)
</script>
<style scoped lang="scss"></style>
