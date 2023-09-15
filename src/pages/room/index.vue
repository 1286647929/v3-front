<script setup lang="ts">
definePage({
	name: '/room',
	path: '/room',
	meta: {
		isShow: false,
	},
})

const emits = defineEmits(['handleChange'])
onMounted(() => {
	emits('handleChange', false)
})
</script>

<template>
	<div>房间</div>
</template>

<style scoped lang="scss"></style>
