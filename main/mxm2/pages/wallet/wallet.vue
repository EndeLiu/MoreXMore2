<template>
	<view>
		<view>这里是钱包页面</view>
		<view v-for="(item, index) in walletData" :key="index" class="account-item-container">
			<AccountItem 
				:value="item.value" 
				:labels="item.labels" 
				:desc="item.desc"
				:wallet="item.wallet"
			/>
		</view>
		
	</view>
</template>

<script>
	import AccountItem from '../../components/AccountItem.vue'
	import {walletData} from '../../test/walletData.js'
	export default {
		components: {
			AccountItem
		},
		data() {
			console.log(walletData)
			return {
				walletData: walletData
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	.account-item-container {
		padding: 20rpx 40rpx;
	}
</style>
