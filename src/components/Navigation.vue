<script setup lang="ts">
import { getRoutes } from '@/plugins/router'
// import { SwitchIcon } from 'vue-dark-switch'

const { t } = useI18n()

/**
 * 获取路由
 */
const routes = getRoutes()
	.filter((r) => !r.path.includes('notFound'))
	.map((r) => {
		let { path, name } = r
		if (path === '/') {
			return { path, name: 'home' }
		}

		if (!name) {
			name = path
		}

		return { path, name: name.toString().slice(1).replaceAll('/', ' · ') }
	})
const activeIndex = ref('1')
const handleSelect = (key: string, keyPath: string[]) => {
	console.log(key, keyPath)
}
</script>

<template>
	<!--			<li v-for="r of routes" :key="r.path" class="hidden !block">-->
	<!--				<RouterLink class="rounded-lg px-3 py-2" :to="r.path">-->
	<!--					{{ t(r.name) }}-->
	<!--				</RouterLink>-->
	<!--			</li>-->
	<el-menu
		:default-active="activeIndex"
		mode="horizontal"
		:ellipsis="false"
		:router="true"
		@select="handleSelect"
	>
		<el-menu-item
			v-for="r of routes"
			:key="r.path"
			:index="r.path"
			:route="r.path"
		>
			{{ t(r.name) }}
		</el-menu-item>
		<div class="flex-grow" />
		<el-menu-item>hao</el-menu-item>
	</el-menu>
</template>

<style scoped="scoped" lang="scss">
.flex-grow {
	flex-grow: 1;
}
</style>
