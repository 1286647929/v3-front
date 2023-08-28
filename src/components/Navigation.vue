<script setup lang="ts">
import { getRoutes } from '@/plugins/router'
import { SwitchIcon } from 'vue-dark-switch'
import { Search } from '@element-plus/icons-vue'

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

const msg = ref('')
</script>

<template>
	<div class="header">
		<div class="header-switch">
			<SwitchIcon unmount-persets />
		</div>
		<div class="header-logo">
			<el-image
				style="width: 188px; height: 49px"
				src="https://res.tuwan.com/templet/play/index/images/yuewanlogo3.png"
			></el-image>
		</div>
		<div class="header-navtabs">
			<el-menu
				:default-active="active"
				active-text-color="#fa6543"
				mode="horizontal"
				:router="true"
				@select="handleSelect"
			>
				<el-menu-item
					v-for="(r, index) of routes"
					:key="r.path"
					:index="index.toString()"
					:route="r.path"
					class="menu_header"
				>
					{{ t(r.name) }}
				</el-menu-item>
			</el-menu>
		</div>
		<div class="header-searchbox">
			<el-input
				v-model="msg"
				class="header-searchbox--input"
				type="text"
				:suffix-icon="Search"
				placeholder="搜索房间/用户昵称"
			></el-input>
		</div>
		<div class="header-iconbtns">
			<div>消息</div>
			<div>{{ t('Registration/Login') }}</div>
			<Dropdown />
		</div>
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
	width: 20px;
	margin-left: 25px;
	font-size: 18px;
}

.el-menu-item:hover {
	outline: 0 !important;
	color: #fa6543 !important;
	background: #ffffff !important;
}

.el-menu-item.is-active {
	color: #fa6543 !important;
	background: #ffffff !important;
}

.header {
	margin-top: 10px;
	text-align: center;
	display: flex;

	.header-switch {
		display: flex;
	}

	.header-logo {
		flex: 0.15;
		text-align: right;
	}

	.header-navtabs {
		flex: 0.3;
	}

	.header-searchbox {
		display: flex;
		justify-content: center;
		align-items: center;
		flex: 0.1;

		:deep(.el-input__wrapper) {
			border-radius: 25px;
		}
	}

	.header-iconbtns {
		flex: 0.5;
		display: flex;
		text-align: center;
		justify-content: right;
	}
}
</style>
