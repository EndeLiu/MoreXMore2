<template>
	<view class="content">
		<view class="page-container"></view>
		<u-tabbar v-model="current" :list="list" :mid-button="true"></u-tabbar>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [{
					iconPath: "../../static/tabIcon/wallet.png",
					selectedIconPath: "../../static/tabIcon/wallet_active.png",
					text: '钱包',
					count: 0,
					isDot: true,
					customIcon: false,
				},
				{
					iconPath: "https://cdn.uviewui.com/uview/common/min_button.png",
					selectedIconPath: "https://cdn.uviewui.com/uview/common/min_button_select.png",
					text: '记账',
					midButton: true,
					customIcon: false,
				},
				{
					iconPath: "account",
					selectedIconPath: "account-fill",
					text: '我的',
					count: 0,
					isDot: false,
					customIcon: false,
				},
			],
			current: 0
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
