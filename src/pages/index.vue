<template>
	<div class="index p-flex p-width-100 p-flex-dir-col p-flex-ac">
		<div class="index-content">
			<el-carousel
				height="264px"
				:interval="5000"
				arrow="always"
				trigger="click"
			>
				<el-carousel-item
					v-for="item in swiperList"
					:key="item"
					@click="testhandler(item.id)"
				>
					<a href="#">
						<el-image :src="item.src" />
					</a>
				</el-carousel-item>
			</el-carousel>
			<div class="p-flex" style="padding: 30px 0">
				<div class="index-content-box hotgames">
					<div class="p-flex p-flex-ac">
						<div class="index-content-box-title">热门游戏</div>
						<a
							href="https://y.tuwan.com/roomlist/"
							target="_blank"
							class="index-content-box-more"
							>更多</a
						>
					</div>
					<div class="p-flex index-content-box-list gamelist">
						<a
							href="https://y.tuwan.com/roomlist?navid=7"
							target="_blank"
							class="p-flex p-flex-dir-col game-item p-flex-center"
							data-navid="7"
						>
							<div
								class="game-img"
								style="
									background-image: url('https://img3.tuwandata.com/uploads/play2/banner/1782141619091963.png');
								"
							></div>
							<div class="game-name">在线LOL</div>
						</a>

						<a
							href="https://y.tuwan.com/roomlist?navid=9"
							target="_blank"
							class="game-item p-flex p-flex-dir-col p-flex-center"
							data-navid="9"
						>
							<div
								class="game-img"
								style="
									background-image: url('https://img3.tuwandata.com/uploads/play2/banner/1175091619093368.png');
								"
							></div>
							<div class="game-name">王者荣耀</div>
						</a>

						<a
							href="https://y.tuwan.com/roomlist?navid=13"
							target="_blank"
							class="game-item p-flex p-flex-dir-col p-flex-center"
							data-navid="13"
						>
							<div
								class="game-img"
								style="
									background-image: url('https://img3.tuwandata.com/uploads/play2/banner/6931001627265307.png');
								"
							></div>
							<div class="game-name">永劫</div>
						</a>

						<a
							href="https://y.tuwan.com/roomlist?navid=11"
							target="_blank"
							class="game-item p-flex p-flex-dir-col p-flex-center"
							data-navid="11"
						>
							<div
								class="game-img"
								style="
									background-image: url('https://img3.tuwandata.com/uploads/play2/banner/5353331619095885.png');
								"
							></div>
							<div class="game-name">LOL手游</div>
						</a>

						<a
							href="https://y.tuwan.com/roomlist?navid=12"
							target="_blank"
							class="game-item p-flex p-flex-dir-col p-flex-center"
							data-navid="12"
						>
							<div
								class="game-img"
								style="
									background-image: url('https://img3.tuwandata.com/uploads/play2/banner/1389341619401234.png');
								"
							></div>
							<div class="game-name">狼人杀</div>
						</a>

						<a
							href="https://y.tuwan.com/roomlist?navid=3"
							target="_blank"
							class="game-item p-flex p-flex-dir-col p-flex-center"
							data-navid="3"
						>
							<div
								class="game-img"
								style="
									background-image: url('https://img3.tuwandata.com/uploads/play2/banner/6883531619091181.png');
								"
							></div>
							<div class="game-name">听歌</div>
						</a>
					</div>
				</div>
				<div class="index-content-box recommend">
					<div class="index-content-box-title">富豪推荐</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
// const { t } = useI18n()
const swiperList = ref([
	{
		id: 1,
		src: 'https://img3.tuwandata.com/uploads/play2/banner/2500761647091618.jpg',
	},
	{
		id: 2,
		src: 'https://img3.tuwandata.com/uploads/play2/banner/2500761647091618.jpg',
	},
	{
		id: 3,
		src: 'https://img3.tuwandata.com/uploads/play2/banner/2500761647091618.jpg',
	},
	{
		id: 4,
		src: 'https://img3.tuwandata.com/uploads/play2/banner/2500761647091618.jpg',
	},
])

const testhandler = (id) => {
	console.log(id)
}
</script>
<style scoped lang="scss">
.index {
	background-image: url(https://res.tuwan.com/templet/play/index/images/newbanner-1.jpg?v=1);
	background-position: top;
	background-repeat: repeat-x;
	min-height: calc(100vh - 308px);
	background-size: 1920px 491px;

	.index-content {
		min-width: 1200px;
		width: 1200px;
		margin: 0 auto;
		padding-top: 25px;
		padding-bottom: 60px;
	}
}

.p-width-100 {
	width: 100%;
}

.p-flex {
	display: flex;
}

.p-flex-ac {
	align-items: center;
}

.p-flex-dir-col {
	flex-direction: column;
}

.index-content-box-title {
	font-size: 16px;
	line-height: 20px;
	color: #fff;
	height: 20px;
	letter-spacing: 2px;
}

.index-content-box-more {
	font-size: 12px;
	color: #fff;
	padding: 0 14px;
	height: 20px;
	line-height: 18px;
	border: 1px solid #fff;
	text-decoration: none;
	border-radius: 20px;
	cursor: pointer;
	margin-left: auto;
	display: block;
}

.index-content-box-list.gamelist {
	width: 480px;
}
.index-content-box-list {
	margin-top: 20px;
}

.index-content-box-list.gamelist .game-item {
	width: 60px;
	font-size: 14px;
	color: #fff;
	cursor: pointer;
	margin-right: 24px;
}

.p-flex-center {
	align-items: center;
}

.index-content-box-list.gamelist .game-item .game-img {
	width: 60px;
	height: 60px;
	background-repeat: no-repeat;
	background-size: 100% auto;
	background-position-y: -160px;
	transition: all 0.3s ease;
}

.index-content-box-list.gamelist .game-item .game-name {
	line-height: 14px;
	height: 14px;
	margin-top: 18px;
	white-space: nowrap;
}

.index-content-box .recommend {
	margin: 0 auto;
}
</style>
