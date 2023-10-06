<template>
	<div class="index p-flex p-width-100 p-flex-dir-col p-flex-ac">
		<div class="index-content">
			<!--			广告栏-->
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
			<!--			热门游戏、推荐-->
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
							v-for="item in gamelist"
							:key="item.id"
							href="#"
							class="p-flex p-flex-dir-col game-item p-flex-center"
						>
							<div
								class="game-img"
								:style="{ backgroundImage: 'url(' + item.src + ')' }"
							></div>
							<div class="game-name">{{ item.name }}</div>
						</a>
					</div>
				</div>
				<div class="index-content-box recommend">
					<div class="index-content-box-title">富豪推荐</div>
					<div class="index-content-box-card">
						<el-carousel
							height="150px"
							:interval="4000"
							indicator-position="none"
							type="card"
							trigger="click"
						>
							<el-carousel-item v-for="item in 6" :key="item">
								<el-image
									src="https://ucavatar2.tuwan.com/data/avatar/003/90/87/14_avatar_middle.jpg?random=1693337148&amp;x-oss-process=image/resize,m_fill,h_120,w_120"
								/>
								<el-text style="display: block; color: #fff" size="large"
									>昵称</el-text
								>
							</el-carousel-item>
						</el-carousel>
					</div>
				</div>
			</div>
			<!--开黑栏目、标签-->
			<div class="p-flex p-width-100 p-flex-ac">
				<div class="p-flex p-flex-ac index-content-block-tags">
					<div
						class="index-content-block-title gameicon"
						style="
							background-image: url('https://img3.tuwandata.com/uploads/repayment/20210422/20210422_1619099029_83253.png');
						"
					>
						免费开黑
					</div>
					<div class="index-content-block-tags p-flex p-flex-ac">
						<div
							v-for="item in tagsList"
							:key="item.id"
							:class="item.tagsClass"
							@click="handlertagclass(item)"
						>
							{{ item.name }}
						</div>
					</div>
					<a
						class="index-content-block-more"
						href="https://y.tuwan.com/chatroom/32820?r=20201125"
						target="_blank"
						>更多</a
					>
				</div>
			</div>
			<div class="p-flex index-content-block-roomlist">
				<a
					v-for="(item, index) in 10"
					:key="index"
					class="room-item"
					@click="handlertoRoom(item)"
				>
					<div class="room-item-voicewave"></div>
					<div class="room-item-cover">
						<el-image
							src="https://img3.tuwandata.com/uploads/chatroom/20221009/1386971665278402.jpg"
						/>
					</div>
					<div class="room-item-info">
						<div class="room-item-info-roomname p-text-over">LOLฅ猫咖馆ฅ</div>
						<div class="p-flex p-flex-ac">
							<el-image
								class="fl room-item-info-avatar"
								src="https://ucavatar3.tuwan.com/data/avatar/004/57/71/87_avatar_middle.jpg?random=20230903&x-oss-process=image/resize,m_fill,h_120,w_120"
							></el-image>
							<div class="fl p-text-over room-item-info-hostname">
								ℒucky▸公主
							</div>
							<el-image
								class="fl room-item-info-chatgif"
								src="https://res.tuwan.com/templet/play/index/images/chat.gif"
							/>
							<div class="fr room-item-info-num">82人</div>
						</div>
					</div>
				</a>
			</div>
		</div>
	</div>
</template>

<script setup>
// const { t } = useI18n()
const router = useRouter()

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

const gamelist = ref([
	{
		id: 1,
		name: '在线LOL',
		src: 'https://img3.tuwandata.com/uploads/play2/banner/1782141619091963.png',
	},
	{
		id: 2,
		name: '王者荣耀',
		src: 'https://img3.tuwandata.com/uploads/play2/banner/1175091619093368.png',
	},
	{
		id: 3,
		name: '永劫',
		src: 'https://img3.tuwandata.com/uploads/play2/banner/6931001627265307.png',
	},
	{
		id: 4,
		name: 'LOL手游',
		src: 'https://img3.tuwandata.com/uploads/play2/banner/5353331619095885.png',
	},
	{
		id: 5,
		name: '狼人杀',
		src: 'https://img3.tuwandata.com/uploads/play2/banner/1389341619401234.png',
	},
	{
		id: 6,
		name: '听歌',
		src: 'https://img3.tuwandata.com/uploads/play2/banner/6883531619091181.png',
	},
])

const tagsclass = ref('tag p-flex p-flex-center')
const tagsclass_active = ref('tag p-flex p-flex-center active')

const tagsList = ref([
	{
		id: 1,
		name: '热门',
		tagsClass: tagsclass_active.value,
	},
	{
		id: 2,
		name: '在线LOL',
		tagsClass: tagsclass.value,
	},
	{
		id: 3,
		name: '绝地求生',
		tagsClass: tagsclass.value,
	},
	{
		id: 4,
		name: '永劫',
		tagsClass: tagsclass.value,
	},
])

// const activeName = ref('first')

/**
 * 切换标签颜色
 * @param item
 */
const handlertagclass = (item) => {
	// console.log(item)
	tagsList.value.forEach((item) => {
		item.tagsClass = tagsclass.value
	})
	item.tagsClass = tagsclass_active.value
	// tagsList.value
}

const testhandler = (id) => {
	console.log(id)
}

/**
 * 切换房间
 * @param item
 */
const handlertoRoom = (item) => {
	console.log(item)
	router.push({
		path: '/room',
		query: {
			id: item,
		},
	})
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

.index-content-box.recommend {
	width: 100%;
	margin: 0 80px;
}

.index-content-box-card {
	text-align: center;
}

.index-content-block-title.gameicon {
	background-position: 0;
	background-repeat: no-repeat;
	background-size: 40px auto;
	padding-left: 51px;
	border-left: none;
	font-size: 24px;
	color: #333;
}

.index-content-block-title {
	font-size: 22px;
	color: #6a6a6a;
	height: 40px;
	line-height: 40px;
	padding-left: 8px;
	border-left: 6px solid #fa6544;
	white-space: nowrap;
}

.index-content-block-tags {
	width: 100%;
}

.index-content-block-tags .tag {
	padding: 0 14px;
	height: 26px;
	color: #6a6a6a;
	border: 1px solid #dadada;
	border-radius: 13px;
	cursor: pointer;
	font-size: 16px;
	margin-left: 17px;
	white-space: nowrap;
}

.index-content-block-tags .tag.active,
.index-content-block-tags .tag:hover {
	color: #fa6544;
	border: 1px solid #fa6544;
}

.index-content-block-more,
.index-content-block-refresh {
	font-size: 16px;
	font-weight: 400;
	cursor: pointer;
	margin-left: auto;
	display: block;
}

.index-content-block-more {
	padding-right: 12px;
	height: 26px;
	background: url(https://res.tuwan.com/templet/play/index/images/right_arrow_ygb.png)
		no-repeat 100%;
	line-height: 26px;
	color: #666;
	flex-shrink: 0;
}

.index-content-block-roomlist {
	flex-wrap: wrap;
}

.room-item {
	width: 220px;
	margin-top: 20px;
	margin-right: auto;
	cursor: pointer;
	display: block;
	position: relative;
	background: #fff;
	border-radius: 5px;
	overflow: hidden;
	transition: all 0.3s ease; //浮动过程所需要的时间
}

.room-item:hover {
	width: 220px;
	margin-top: 20px;
	margin-right: auto;
	cursor: pointer;
	display: block;
	position: relative;
	background: #fff;
	border-radius: 5px;
	overflow: hidden;
	transform: translate(0, -10px); //向上浮动
}

.room-item-voicewave {
	width: 220px;
	height: 186px;
	position: absolute;
	z-index: 2;
}

.room-item-voicewave:hover {
	width: 220px;
	height: 186px;
	background-image: url(https://res.tuwan.com/templet/play/index/images/voicewave.gif?v=1);
	background-position: 50%;
	background-repeat: no-repeat;
	background-color: rgba(51, 51, 51, 0.2);
	background-size: 100% 100%;
	position: absolute;
	left: 0;
	top: 0;
	z-index: 2;
}

.room-item-cover {
	width: 100%;
	background: #fbfbfb;
}

.room-item-info {
	color: #999;
	font-size: 14px;
	padding: 10px 12px;
}
.room-item-info-roomname {
	color: #333;
	font-size: 16px;
	height: 16px;
	line-height: 16px;
	margin-bottom: 6px;
}

.p-text-over {
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
}

.room-item-info-avatar {
	width: 24px;
	height: 24px;
	border-radius: 100%;
}

.room-item-info-hostname {
	margin-left: 7px;
	height: 14px;
	line-height: 14px;
}

.p-text-over {
	overflow: hidden;
	white-space: nowrap;
	text-overflow: ellipsis;
}

.room-item-info-chatgif {
	width: 10px;
	height: 10px;
	margin-left: 5px;
}

.room-item-info-num {
	margin-left: auto;
	height: 14px;
	line-height: 14px;
	white-space: nowrap;
	width: max-content;
}
</style>
