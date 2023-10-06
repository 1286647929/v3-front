<script setup lang="ts">
const router = useRouter()

definePage({
	name: 'room',
	path: '/room',
	meta: {
		isShow: false,
	},
})

const emits = defineEmits(['handleChange'])
onMounted(() => {
	emits('handleChange', false)
})

const goHome = () => {
	router.push('/')
}
</script>

<template>
	<div class="wrap">
		<el-container>
			<el-header class="header">
				<el-row class="header-wrap">
					<el-col class="header-wrap-left" :span="3">
						<div class="wrap-left-userinfo">
							<el-avatar
								src="https://qiniu.shijitianchen.com/android_164665_20220505_105131_7197242?imageView2/2/w/200/h/200/format/png/q/75"
							></el-avatar>
							<span style="margin-left: 10px">NH⁷ෆ醉美</span>
						</div>
					</el-col>
					<el-col class="header-wrap-center" :span="16"></el-col>
					<el-col class="header-wrap-right" :span="5">
						<div class="wrap-right-tag">
							<div class="tag-message" />
							<div class="tag-name">我的消息</div>
						</div>
						<div class="wrap-right-tag" @click="goHome">
							<div class="tag-home" />
							<div class="tag-name">返回首页</div>
						</div>
					</el-col>
				</el-row>
			</el-header>
			<el-container>
				<el-aside class="aside-left">
					<div class="aside-left-wrap">
						<div class="top-chat-btn">
							<div class="text-btn">更多聊天室</div>
							<div class="btn">
								<el-image
									src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAaCAMAAACelLz8AAAAgVBMVEUAAAD///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////9d3yJTAAAAK3RSTlMAAQQHCAkLEhQiIyQlLDEyOTo8PT4/QEFCREVGR0hNUXx9foGCg6CusLO1RjAeqAAAAP1JREFUKM99kuuSwiAMhdFarbJUIQm1rdZr3bXv/4Bydd1uh/OHGT6SHOAw5jTLVutyB7Ar16tsxj40L4QEqowIpCjmv2TBpa4q7WRWyReRLAWG/UBRLD3JBf0hhpHI3RyOI2LruJ1XyH/EMFkwlgk9KZFNF/kyDh6RArILKHIIONv6U7TvaiRNWHd7x/SWhX6qe/RHRerYPzrlO7LQD5rb0B/koR9uDfiOERG21+f9dH9eWwzDYkMzvzkP38O5AQoWow3L2svPpQ3E2ojmtXNXYyAVfH1emVBF4q6ceKjE86Y+JfGVqQBMxCYfhU3bsOlR2FxEN6VElOXmHdEXGt8uz36Mu5oAAAAASUVORK5CYII="
								></el-image>
							</div>
						</div>
					</div>
				</el-aside>
				<el-main class="main"> 主要 </el-main>
				<el-aside> 旁边的旁边 </el-aside>
			</el-container>
		</el-container>
	</div>
</template>

<style scoped lang="scss">
.wrap {
	width: 100%;
	height: 100vh;
	display: flex;
	background-image: url(http://qiniu.shijitianchen.com/admin/20220803/8ecc67bb0f2240a5c5bafdf320672b37.jpg);

	.header {
		padding: 0;
		width: 100%;

		.header-wrap {
			height: 100%;
			display: flex;

			.header-wrap-left {
				display: flex;
				align-items: center;
				color: white;

				.wrap-left-userinfo {
					display: flex;
					margin-left: 10px;
					overflow: hidden;
					align-items: center;
				}
			}

			.header-wrap-center {
				//background: #0047e1;
			}

			.header-wrap-right {
				width: 364px;
				display: flex;
				align-items: center;
				justify-content: flex-end;

				.wrap-right-tag {
					font-size: 12px;
					color: hsla(0, 0%, 100%, 0.58);
					margin-right: 10px;
					cursor: pointer;
					margin: 0 12px;

					.tag-home {
						height: 22px;
						background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABYAAAAVCAYAAABCIB6VAAACDElEQVRIS52VWWsUURCFv+OGy5ug5kFQVBQR9x1xQXFB8Rf4O1VcgsFIgsYQwWDEHQwRfPLFIG5HjtwZetqe6YkFA9N9q76pe+reM2KIsL0POAgsA55LetpWprYE20eAQ7W8WUkTg2oHgm0fAI4VwBzwE9hbnp9JetIP3hdsew9wqhTOSJrKd9v7gePl/ZSkmSZ4I9j2LuAMkPVoOlkttn0YyCcxIWm2Dv8HbHs7cL5A5ySNN3VkO12newPjkl5W83rAtrcAF8v0XwNjklLYGLYjVSRLzgNJbzqJXbDtzcBlYDnwDhgdBO0AbJ8FIt1v4L6kD1n7C7Y9AlwFVgCfgJuSktgatsOIdJHwF3BH0rxsbwCuAasK5WFdrza67VycSBgpcyRvBXwDWFcpjq6v2mD19QK/AkTSxYDzsLJou7EMbMngImmkPNfVuLy8BGz9H3DReQewIOlrK9h2dpKtRcNqZLDzkn6UpqJtTtRbSaN18IUy2a7GtuNoR/vo3fUK2zuLBB8l3R4GHAOKES0CXyo/kE7jH59Lx0sGnwDixQOdbNiOc+9jkbk4J4tNTkuaHnC1dwOngUYpckyypQUgPpsBRYZtQA/Y9mpgTRlqLCB/Bhnye0n36hp3dGpqrOu7tjcB1xtOSuoeSXrRAy5bz7BiKOmmE9+Bu5Kyk8izvvjK2krONyCX6nHHuP4AxS/sxe+EWOQAAAAASUVORK5CYII=)
							50% no-repeat;
					}

					.tag-message {
						height: 22px;
						background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABYAAAATCAMAAACjpw26AAAAjVBMVEUAAAD///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////8DizOFAAAAL3RSTlMAAQIEBQkPERIWGx4kKSosLS4wMzQ1Ojs8PUFFSUpMTU9QU1VWWVpbXV5gYWJlZlmrcm8AAACcSURBVBjTnY5bE0JgGIRXyCGniFDyySGH7P//eRkzpeHOc7fPzO77Qgo7ruhCCSFFvEIwRCewQXRgvNUx92g31aFEkQI9dRdtkAUCMkBBGj+tjczgkR4yjtoyYvoqJNuWoPrmrk+SrU6IppTXVi4bOGyLicsUz6KYaekAVl5V1buGcuOrmsmtb+9RH0teD+u5+9AP1vb2qX9q//kDqrkWtEwfU48AAAAASUVORK5CYII=)
							50% no-repeat;
					}

					.tag-name {
						margin-top: 10px;
					}
				}

				.wrap-right-tag:hover {
					font-size: 12px;
					color: white;
					margin-right: 10px;
					cursor: pointer;
					margin: 0 12px;

					.tag-home {
						height: 22px;
						background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABYAAAAVCAYAAABCIB6VAAACDElEQVRIS52VWWsUURCFv+OGy5ug5kFQVBQR9x1xQXFB8Rf4O1VcgsFIgsYQwWDEHQwRfPLFIG5HjtwZetqe6YkFA9N9q76pe+reM2KIsL0POAgsA55LetpWprYE20eAQ7W8WUkTg2oHgm0fAI4VwBzwE9hbnp9JetIP3hdsew9wqhTOSJrKd9v7gePl/ZSkmSZ4I9j2LuAMkPVoOlkttn0YyCcxIWm2Dv8HbHs7cL5A5ySNN3VkO12newPjkl5W83rAtrcAF8v0XwNjklLYGLYjVSRLzgNJbzqJXbDtzcBlYDnwDhgdBO0AbJ8FIt1v4L6kD1n7C7Y9AlwFVgCfgJuSktgatsOIdJHwF3BH0rxsbwCuAasK5WFdrza67VycSBgpcyRvBXwDWFcpjq6v2mD19QK/AkTSxYDzsLJou7EMbMngImmkPNfVuLy8BGz9H3DReQewIOlrK9h2dpKtRcNqZLDzkn6UpqJtTtRbSaN18IUy2a7GtuNoR/vo3fUK2zuLBB8l3R4GHAOKES0CXyo/kE7jH59Lx0sGnwDixQOdbNiOc+9jkbk4J4tNTkuaHnC1dwOngUYpckyypQUgPpsBRYZtQA/Y9mpgTRlqLCB/Bhnye0n36hp3dGpqrOu7tjcB1xtOSuoeSXrRAy5bz7BiKOmmE9+Bu5Kyk8izvvjK2krONyCX6nHHuP4AxS/sxe+EWOQAAAAASUVORK5CYII=)
							50% no-repeat;
					}

					.tag-message {
						height: 22px;
						background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABYAAAATCAMAAACjpw26AAAAjVBMVEUAAAD///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////8DizOFAAAAL3RSTlMAAQIEBQkPERIWGx4kKSosLS4wMzQ1Ojs8PUFFSUpMTU9QU1VWWVpbXV5gYWJlZlmrcm8AAACcSURBVBjTnY5bE0JgGIRXyCGniFDyySGH7P//eRkzpeHOc7fPzO77Qgo7ruhCCSFFvEIwRCewQXRgvNUx92g31aFEkQI9dRdtkAUCMkBBGj+tjczgkR4yjtoyYvoqJNuWoPrmrk+SrU6IppTXVi4bOGyLicsUz6KYaekAVl5V1buGcuOrmsmtb+9RH0teD+u5+9AP1vb2qX9q//kDqrkWtEwfU48AAAAASUVORK5CYII=)
							50% no-repeat;
					}

					.tag-name {
						margin-top: 10px;
					}
				}
			}
		}
	}

	.aside-left {
		width: 280px;
		height: 100%;
		display: flex;
		flex-direction: column;

		.aside-left-wrap {
			display: flex;
			justify-content: center;

			.top-chat-btn {
				width: 151px;
				height: 30px;
				background-image: url(data:image/png;base64,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);
				display: flex;
				cursor: pointer;
				//justify-content: center;
				align-items: center;

				.text-btn {
					color: white;
					margin-left: 38px;
				}

				.btn {
					display: flex;
					margin-left: 17px;
				}
			}
		}
	}

	.main {
		padding: 0;
	}
}
</style>
