<script setup lang="ts"></script>

<template>
	<div class="footer p-width-100 p-flex p-flex-dir-col">
		<div class="footer-footer_box">
			<div class="p-flex footer-help_box p-flex-jc">
				<div class="p-flex footer-help_box-border_right p-flex-ac">
					<i class="footer-help_box-icon footer-help_box-custom"></i>
					<span>客服电话：</span>
					<span class="footer-help_box-custom_01">XXXX-XXXX-XXXX</span>
					<span class="footer-help_box-custom_02">咨询时间：7X24小时</span>
				</div>
				<div class="p-flex p-flex-ac" style="padding-left: 30px">
					<i class="footer-help_box-icon footer-help_box-QQ" />
					<span>客服QQ：</span>
					<span class="footer-help_box-custom_01">XXXX</span>
					<span class="footer-help_box-custom_02">咨询时间：7X24小时</span>
				</div>
				<div class="p-flex p-flex-ac" style="margin-left: 40px">
					<a href="#" class="footer-help_box-help">帮助中心</a>
					<a href="#" class="footer-help_box-help">关于我们</a>
				</div>
			</div>
			<div
				class="p-flex footer-copy p-flex-center"
				style="justify-content: center"
			>
				<span
					>电话号码：XXXX-XXXX-XXXX&nbsp;&nbsp;公司地址：XXXXXXX&nbsp;&nbsp;公司全称：Ay科技有限公司&nbsp;&nbsp;备案号：</span
				>
				<a class="footer-wenww" href="http://beian.miit.gov.cn/"
					>京ICP备15050374号-1</a
				>
			</div>
		</div>
	</div>
</template>

<style scoped lang="scss">
.p-flex {
	display: flex;
}

.p-flex-dir-col {
	flex-direction: column;
}

.p-width-100 {
	width: 100%;
}

.p-flex-ac {
	align-items: center;
}

.footer {
	background-color: #535353;
	position: relative;
	padding: 30px 0;

	.footer-footer_box {
		width: 1204px;
		margin: 0 auto;
		background-color: #535353;

		.footer-help_box {
			color: #c9c9c9;
			font-size: 15px;
		}

		.p-flex-jc {
			justify-content: center;
		}

		.footer-help_box-border_right {
			border-right: 1px solid #bfbfbf;
			margin-left: 35px;
			padding-right: 30px;
		}

		.footer-help_box-icon {
			background: url(https://asset.tuwan.com/static/img/icon.e086bd7d.png)
				no-repeat;
			transition: all 0.3s ease;
			display: inline-block;
			margin-right: 10px;
		}

		.footer-help_box-custom_01 {
			font-size: 17px;
			margin-right: 14px;
		}

		.footer-help_box-custom_02 {
			font-size: 13px;
		}

		.footer-help_box-custom {
			height: 18px;
			width: 23px;
			background-position: -108px 0;
		}

		.footer-help_box-QQ {
			height: 18px;
			width: 19px;
			background-position: -89px 0;
		}

		.footer-help_box-help {
			width: 92px;
			height: 26px;
			background-color: #3c3c3c;
			line-height: 26px;
			text-align: center;
			border: 1px solid #707070;
			border-radius: 4px;
			margin-left: 16px;
			font-size: 13px;
			color: #bfbfbf;
		}

		.footer-copy {
			color: #959595;
			font-size: 12px;
			margin-top: 34px;
			text-align: center;
		}

		.footer-wenww {
			color: #959595;
		}
	}
}
</style>
