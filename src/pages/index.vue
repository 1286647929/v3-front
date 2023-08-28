<template>
	<div
		style="
			width: 100%;
			background-color: #faaca8;
			background-image: linear-gradient(19deg, #faaca8 0%, #ddd6f3 100%);
			height: 350px;
		"
	>
		<div
			style="
				width: 100%;
				display: flex;
				align-items: center;
				justify-content: center;
				margin-top: 18px;
			"
		>
			<div style="width: 50%">
				<el-carousel :interval="5000" arrow="always">
					<el-carousel-item v-for="item in 4" :key="item">
						<h3 text="2xl">{{ item }}</h3>
					</el-carousel-item>
				</el-carousel>
			</div>
		</div>
	</div>
</template>

<script setup>
// const { t } = useI18n()
</script>
<style scoped lang="scss">
.el-carousel__item h3 {
	color: #475669;
	opacity: 0.75;
	line-height: 300px;
	margin: 0;
	text-align: center;
}

.el-carousel__item:nth-child(2n) {
	background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
	background-color: #d3dce6;
}
</style>
