<script setup lang="ts">
import { getRoutes } from '@/plugins/router'
import { SwitchIcon } from 'vue-dark-switch'

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
const handleSelect = (key: string, keyPath: string[]) => {
	console.log(key, keyPath)
}

const active = ref('0')
</script>

<template>
	<!--			<li v-for="r of routes" :key="r.path" class="hidden !block">-->
	<!--				<RouterLink class="rounded-lg px-3 py-2" :to="r.path">-->
	<!--					{{ t(r.name) }}-->
	<!--				</RouterLink>-->
	<!--			</li>-->
	<div style="margin-top: 20px; flex: 1">
		<el-menu
			:default-active="active"
			mode="horizontal"
			:ellipsis="false"
			:router="true"
			@select="handleSelect"
		>
			<span class="h-10 w-10 flex items-center justify-center">
				<SwitchIcon unmount-persets />
			</span>
			<div>
				<el-image
					style="margin-left: 80px; margin-bottom: 12px; margin-right: 10px"
					src="https://res.tuwan.com/templet/play/index/images/yuewanlogo3.png"
				></el-image>
			</div>
			<el-menu-item
				v-for="(r, index) of routes"
				:key="r.path"
				:index="index.toString()"
				:route="r.path"
				class="menu_header"
			>
				{{ t(r.name) }}
			</el-menu-item>
			<div class="flex-grow" />
			<el-menu-item>{{ t('Registration/Login') }}</el-menu-item>
			<div class="drop">
				<Dropdown />
			</div>
		</el-menu>
	</div>
</template>

<style scoped lang="scss">
.flex-grow {
	flex-grow: 1;
}

.drop {
	//margin-top: 10px;
	text-align: center;
	vertical-align: center;
}

.menu_header {
	margin-left: 15px;
}
//
//.el-carousel__item h3 {
//	color: #475669;
//	opacity: 0.75;
//	line-height: 300px;
//	margin: 0;
//	text-align: center;
//}
//
//.el-carousel__item:nth-child(2n) {
//	background-color: #99a9bf;
//}
//
//.el-carousel__item:nth-child(2n + 1) {
//	background-color: #d3dce6;
//}
</style>
