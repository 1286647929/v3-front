<script setup lang="ts">
import { getRoutes } from '@/plugins/router'
import { SwitchIcon } from 'vue-dark-switch'
import { Search } from '@element-plus/icons-vue'
// import {useRoute} from 'vue-router'

const { t } = useI18n()
// const route = useRoute()

/**
 * 获取路由
 */
const routes = getRoutes()
	.filter((r) => {
		return !r.path.match(/notFound|test/)
	})
	.filter((r) => {
		return !(!r.meta.isShow && r.meta.isShow != null)
	})
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

const active = ref('0')

const msg = ref('')

const roomeFlag = ref(false)
const loginFlag = ref(false)
const userInfoVisible = ref(false)
const handleRoomeEnter = () => {
	roomeFlag.value = true
}

const handleRoomeLeave = () => {
	roomeFlag.value = false
}

const handleLoginEnter = () => {
	loginFlag.value = true
}

const handleLoginLeave = () => {
	loginFlag.value = false
}

//登录窗口visible
const loginDialogVisible = ref(false)

const handleLogin = () => {
	loginDialogVisible.value = true
}

const callback = (value) => {
	// console.log(value)
	loginDialogVisible.value = value
}

const emits = defineEmits(['handleChange'])
onMounted(() => {
	emits('handleChange', true)
})
</script>

<template>
	<div class="header">
		<!--夜间模式切换-->
		<div class="header-switch">
			<SwitchIcon unmount-persets />
		</div>

		<!--logo-->
		<a class="header-logo" href="/">
			<el-image
				style="width: 188px; height: 49px"
				src="https://res.tuwan.com/templet/play/index/images/yuewanlogo3.png"
			></el-image>
		</a>

		<!--菜单部分-->
		<div class="header-navtabs">
			<el-menu
				:default-active="active"
				active-text-color="#fa6543"
				mode="horizontal"
				:router="true"
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
		<!--搜索部分-->
		<div class="header-searchbox">
			<el-input
				v-model="msg"
				class="header-searchbox--input"
				type="text"
				:suffix-icon="Search"
				placeholder="搜索房间/用户昵称"
			></el-input>
		</div>

		<!--大厅部分-->
		<div class="header-iconbtns">
			<div
				class="header-iconbtns-iconbtn header-iconbtns-chatroom"
				@mouseenter="handleRoomeEnter"
				@mouseleave="handleRoomeLeave"
			>
				<span>大厅</span>
				<div v-if="roomeFlag" class="room-box">
					<div class="room-box-sanjiao" />
					<el-card class="box-card">
						<el-row style="border-bottom: solid 1px #efefef">
							<el-col v-for="(item, index) in 6" :key="item" :span="4">
								<span class="font-bold"> {{ '狼人杀' + index }} </span>
							</el-col>
						</el-row>
						<el-row>
							<el-col
								v-for="i in 6"
								:key="i"
								:span="4"
								class="box-card-roomname"
							>
								<a class="block">1</a>
								<a class="block">2</a>
								<a class="block">3</a>
								<a class="block">4</a>
								<a class="block">5</a>
								<a class="block">6</a>
								<el-button
									style="
										border-radius: 32px;
										color: #a8a8a8;
										background: #f5f5f5;
										margin-top: 10px;
										height: 24px;
										line-height: 24px;
										width: 130px;
									"
									>更多{{ i }}
								</el-button>
							</el-col>
						</el-row>
					</el-card>
				</div>
			</div>

			<div class="divider">
				<el-divider direction="vertical" />
			</div>

			<!--消息部分-->
			<div class="header-iconbtns-iconbtn header-iconbtns-msg">
				<span>消息</span>
			</div>
			<div class="divider">
				<el-divider direction="vertical" />
			</div>

			<!--等待登录部分-->
			<div
				v-if="!userInfoVisible"
				class="header-iconbtns-iconbtn header-iconbtns-login"
				@mouseenter="handleLoginEnter"
				@mouseleave="handleLoginLeave"
				@click="handleLogin"
			>
				<span>{{ t('Registration/Login') }}</span>
				<div v-if="loginFlag" class="login-box">
					<el-card>
						<div style="text-align: left; overflow: hidden">
							<el-text class="block font-bold">登录后可享受：</el-text>
							<el-text class="block">
								<el-icon>
									<Box />
								</el-icon>
								超值大礼包
							</el-text>
							<el-text class="block">
								<el-icon>
									<Goblet />
								</el-icon>
								超值大礼包
							</el-text>
						</div>
						<div
							style="display: flex; justify-content: center; margin-top: 15px"
						>
							<el-button type="success">登录</el-button>
						</div>
					</el-card>
				</div>
			</div>

			<!--登录后用户头像部分-->
			<div v-if="userInfoVisible" class="header-iconbtns-logininfo">
				<div class="usermenu">
					<el-row>
						<el-col :span="8">
							<a href="#">
								<div class="usermenu-info-avatar">
									<el-avatar
										src="https://ucavatar2.tuwan.com/data/avatar/003/92/42/30_avatar_middle.jpg?random=20230911"
									></el-avatar>
								</div>
							</a>
						</el-col>
						<el-col :span="16">
							<div class="usermenu-info-username">
								<span class="nickname">恰恰王ބ</span>
								<div class="rank" />
							</div>
							<div class="usermenu-info-uid">UID:3924230</div>
						</el-col>
					</el-row>
				</div>
			</div>
		</div>
		<!--语言切换-->
		<Dropdown />
	</div>
	<Login :visibale="loginDialogVisible" @change-value="callback" />
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
	border: none;
}

.el-menu {
	border: none;
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
	padding-top: 10px;
	text-align: center;
	display: flex;

	.divider {
		display: flex;
		align-items: center;
	}

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
			background-color: #f0f0f0;
		}
	}

	.header-iconbtns {
		flex: 0.5;
		display: flex;
		text-align: center;
		justify-content: right;
		margin-left: auto;
		margin-right: 4vw;

		.header-iconbtns-iconbtn {
			margin: 0 20px;
			background-position: top;
			background-repeat: no-repeat;
			background-size: contain;
			padding-top: 30px;
			color: #666;
			font-size: 12px;
			text-align: center;
			line-height: 26px;
			display: block;
			width: 36px;
			white-space: nowrap;
			position: relative;
		}

		.header-iconbtns-chatroom {
			background-image: url(https://asset.tuwan.com/static/img/chaticon.807cd48f.gif);
			color: #fa6543;
			font-size: 14px;
		}

		.header-iconbtns-iconbtn:hover {
			color: #fa6543;
			cursor: pointer;
		}

		.header-iconbtns-msg {
			background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB8AAAAZCAYAAADJ9/UkAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAABmJLR0QAAAAAAAD5Q7t/AAAACXBIWXMAAAsSAAALEgHS3X78AAADGElEQVRIx7XWW4hVZRTA8d85DoOUgxmTUWRUjgSBdvECXQwtK0jywZBqwhCmFoQESS/2ElYIXSiLwGiF0MVBKyqKbig2D5GDFN2MICi6kOmDMTbkYFHYw94HTqezz8w0tl725luX/7e/vdb6Vk2LREQ3bsTNuBhnoEt7+R0/4xNsxxuZedwEpdYCvgQ7cADPYigzD3UKEBFzsBx3YwxrM/O7ScEjYnkJ3pCZOya6+yb/Ou7BBlyXmfsnBI+IufgQazLzg8mCWzZxKzbjosw80sm2Xj6fxENTBUNmDuI93DeebT0iFmIBtk4V3CT347aImD3el68tNpx/nChyZh7E+1g1HvwK7DqBX92Qd3EVRETbUu3CHHz9P8C/xfryfV9EHMMzeLHRC+rozcxf23lHxKxO0SOiFhGnVKhH0F2+L1XkwXq8HREnNeD1DvEPR8S0Dvqz8EWFrobjkJljmbkLl+EXPNeAj0ZET0WAL7GkA/x6fFyh68Xh5oXM/At3YH5ErOjCD+jDp20CPICXI2IT9uIQjuI0rFbU8jUV8HmK//4PycxjEfEYBuoYxqXtvDPzVfTjarxeBhvFR4oqWZaZn1XAV2J3hW4PLu/CO9ioosmUXW9SnS8i+rBQcTO2kwM4vY630BMRqycD6ACehqexJTPHKsxqUG9Kgm0RceUUwTU8gpPxRAfTs/FTvTzaYdyEnRFx538E92IQy7AqM//sYH4t9rYOE+cqkmFzZm6rgPTgHEUD6caZWIE12ImNmflbh01Ox34M1Noo+xQJ1p+ZQ03r3eWRrsOPaFxEB7EPg+NNMGU+vKD43bf8q7tl5jeK8toeEac2qbbifMzLzAWZuSgzFyluriNaGkoF+CXMxgAVg2FmDkXEK3gc6yJiiaKZXJCZR1vMp2MxHoyI78uNjODezGy+sB7FLNzQqIKaComIGfgKt5dHPZyZT3Wwn4nzMFMx9fZn5uJSt1QxH87PzJGGTyW8dFpZHvcMzB1vJmvyq+FzPKyYDfcoBtM3m+1qEwh0F0Yz8/mJgJv8LsRrigtmU2ZuabX5G/Y7EiUPHQ0gAAAAAElFTkSuQmCC);
			background-size: 31px 25px;
		}

		.header-iconbtns-msg:hover {
			background-image: url(https://asset.tuwan.com/static/img/chaticon.807cd48f.gif);
			background-size: 31px 25px;
		}

		.header-iconbtns-login {
			width: auto;
			background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABkAAAAaCAYAAABCfffNAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAABmJLR0QAAAAAAAD5Q7t/AAAACXBIWXMAAAsSAAALEgHS3X78AAACGklEQVRIx63VS4iPURjH8c/8k3KXBYmIhZqsZIkNycL9lstKgyOFhGylpJQIuT2hbNQgmQixmNlQFmTjurBxWVnIbVwKi/eUof/7/79j5rc87znP932e5/ye06KJUkpTsRHzMBm/8BK3cCYinjSL0dIg+CAcxlIcwzU8y5+nYAG24Qp2RsTXXkFSSoNxG2+xPiI+luwbiXMYhvkR8b3evloJ/EgGrCoDQES8x3J8xMHKmaSUpuMqWiPiU7N65zPD8QKz6/WoXibrcLQqIGf0ASexoWq55uJGVUAPdeSzlSATFVe0t3qGCVUhA/HjPyAUHqoEeanwQW/VildVITex8D8gixXeqgQ5j60ppaFVo6eURmATztb7Xub4wCisjIhfGiilVFOMltcRsaVqJrAdo3E5j44ywMgMGIJdZfuaDchDWKIw2jU8zWemKHqwGZewu9GALMtERHTjNDqxFw/RjS94lNfuox3fGpW0rCezcCD35SK6chbvFD4aj3GYiWV5bT8uRMTPhpBcouOYhR243qzx+dwM7MuVWRsRb+pC8htyS2GojRHxpVnwf0AtiguzO4M6/4LkDe34jLYqf98kqw6siIgu/jR+s2K4beoLACLiLtbgQkppLNSys/contnvfQH0AN1RTI4TMACrcS8iHvcHoIf24kVKaVoNixT96Fdlc55CWw3T8KC/IVk3MKeGMXjTx2Bleo5JvwEV87OoX3F1QgAAAABJRU5ErkJggg==);
			background-size: 25px 26px;
		}

		.header-iconbtns-login:hover {
			width: auto;
			background-image: url(https://asset.tuwan.com/static/img/chaticon.807cd48f.gif);
			background-size: 25px 26px;
		}

		.room-box {
			width: 920px;
			display: block;
			position: absolute;
			left: -700px;
			top: 64px;
			z-index: 20;
			justify-content: center;
			flex-direction: column;
			cursor: default;

			.room-box-sanjiao {
				margin-left: 246.008px;
				left: 50%;
				top: -24px;
				width: 0;
				height: 0;
				border: 12px solid rgba(0, 0, 0, 0);
				border-bottom-color: #ff6691;
				position: absolute;
			}

			.box-card {
				border-radius: 12px;
				background: #fff;
				padding: 10px 20px;
				line-height: 28px;

				.box-card-roomname:not(:last-child) {
					border-right: solid 1px #efefef;
				}
			}
		}

		.login-box {
			display: block;
			position: absolute;
			cursor: default;
			width: 220px;
			z-index: 10;
			padding-top: 35px;
			left: -69px;
			text-align: left;
		}

		.header-iconbtns-logininfo {
			margin: 0 20px;
			display: flex;
			align-items: center;

			.usermenu {
				//display: flex;
				width: 162px;

				.usermenu-info-username {
					display: flex;
					text-align: left;
					align-items: center;
				}

				.nickname {
					width: 60px;
					white-space: nowrap;
					overflow: hidden;
					text-overflow: ellipsis;
					font-size: 16px;
					line-height: 18px;
					color: #333;
				}

				.rank {
					margin-left: 5px;
					background-image: url(https://res.tuwan.com/templet/play/public/images/2.png);
					background-repeat: no-repeat;
					background-size: 40px;
					background-position: 50%;
					width: 40px;
					height: 18px;
				}

				.usermenu-info-uid {
					background-image: url(https://res.tuwan.com/templet/play/public/images/common_bottom.png);
					background-repeat: no-repeat;
					background-size: 8px 5px;
					background-position: 100%;
					padding-right: 13px;
					color: #666;
					font-size: 13px;
					margin-top: auto;
					width: max-content;
				}
			}
		}
	}
}
</style>
