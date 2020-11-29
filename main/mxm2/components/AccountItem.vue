<template>
	<view class="account-item">
		<view class="wallet-logo">
			<span>{{walletLogo}}</span>
		</view>
		<view class="labels-desc">
			<view class="labels">
				<view class="label-item" v-for="(item, index) in labels" :key="index">
					{{item}}
				</view>
			</view>
			<view class="desc">
				<view>{{desc}}</view>
			</view>
		</view>
		
		<view class="value" :class="valueType">{{value}}</view>
		
	</view>
</template>

<script>
	export default {
		props: {
			value: {
				default: 0,
				type: Number
			},
			labels: {
				default: () => {
					return []
				},
				type: Array
			},
			desc: {
				default: '',
				type: String
			},
			wallet: {
				default: '',
				type: String
			}
		},
		computed: {
			walletLogo () {
				return this.wallet === '' ? '' : this.wallet[0]
			},
			valueType () {
				return this.value > 0 ? 'in' : 'out'
			}
		},
		data () {
			return {
				a: 123
			}
		}
	}
</script>

<style lang="scss">
	.account-item {
		display: flex;
		align-items: center;
		padding: 20rpx 30rpx;
		box-shadow: 10rpx 0rpx 20rpx rgba(0,0,0,0.1);
		border-radius: 4rpx;
		height: 200rpx;
		.wallet-logo {
			width: 100rpx;
			height: 100rpx;
			background-color: #19BE6B;
			box-shadow: 10rpx 10rpx 20rpx rgba(0,0,0,0.2);
			align-items: center;
			border-radius: 50%;
			span {
				font-size: 50rpx;
				text-align: center;
				display: inline-block;
				width: 100%;
				line-height: 100rpx;
				color: #fff;
			}
		}
		.labels-desc {
			display: flex;
			flex-direction: column;
			margin-left: 20rpx;
			width: 400rpx;
			.labels {
				display: flex;
				margin-bottom: 20rpx;
				.label-item {
					background-color: rgb(212, 238, 252);
					color: rgb(0, 58, 140);
					margin-left: 10rpx;
					padding: 5rpx 20rpx;
					border-radius: 6rpx;
				}
			}
			.desc {

				min-height: 45rpx;
				width: 300rpx;
				border: 4rpx dashed #888;
				text-align: center;
				border-radius: 3rpx;
				line-height: 45rpx;
			}
		}
		.value {
			font-size: 50rpx;
			margin-left: auto;
			font-weight: bolder;
		}
		.in {
			color: #F43F3B;
		}
		.out {
			color: #2B85E4
		}
	}
</style>
