<template>
	<view>
		<view class="item-title">收支金额</view>
		<view class="value-set set-item">
			<view 
				class="value-info" 
				:class="valueType === 1 ? 'value-in' : 'value-out'"
				 @touchstart="touchStart" 
				 @touchend="toucheEnd"
			>
				<view class="type">{{valueTypeText}}</view>
				<view class="value">{{Math.abs(form.value)}}</view>
			</view>
		</view>
		
		<view class="item-title">分类</view>
		<view class="type-set set-item">
			<view class="type-info" @click="showTyleSelector = true">
				<view>{{form.type.main}}</view>
				<view>{{form.type.sub}}</view>
			</view>
			<u-select 
				v-model="showTyleSelector" 
				mode="mutil-column-auto" 
				:list="allTypes" 
				@confirm="setType"
			>
			</u-select>
		</view>
		<view class="item-title">描述</view>
		<view class="desc-set">
			<view class="desc-info">
				<textarea></textarea>
			</view>
		</view>
		<view class="item-title">日期</view>
		<view class="date-set set-item">
			<view class="date-info" @click="showDateSelector = true">
				<view>{{dateSplit[0]}}</view>
				<view>{{dateSplit[1]}}</view>
				<view>{{dateSplit[2]}}</view>
			</view>
			<u-calendar 
				v-model="showDateSelector" 
				mode="date" 
				@change="setDate">
			</u-calendar>
		</view>
		<view class="item-title">支付方式</view>
	</view>
</template>

<script>
	import {testTypes} from '../../test/testTypes.js'
	export default {
		computed: {
			dateSplit () {
				return this.form.date.split('/')
			},
			valueType () {
				return this.form.value >= 0 ? 1 : 0
			},
			valueTypeText () {
				return this.form.value >= 0 ? '收入' : '支出'
			}
		},
		created() {
			const d = new Date()
			this.form.date = d.getFullYear() + '/' + (d.getMonth() + 1) + '/' + d.getDate()
		},
		data() {
			return {
				touchPosition: null,
				form: {
					value: 11,
					type: {
						main: '着装',
						sub: '上衣'
					},
					date: '2020/12/1'
				},
				showDateSelector: false,
				showTyleSelector: false,
				allTypes: testTypes
			}
		},
		methods: {
			setDate (dateObj) {
				const {year, month, day} = dateObj
				this.form.date = `${year}/${month}/${day}`
			},
			setType (typeObj) {
				this.form.type = {
					main: typeObj[0].label,
					sub: typeObj[1].label
				}
			},
			touchStart (e) {
				this.touchPosition = e.touches[0].clientX
			},
			toucheEnd (e) {
				if (this.touchPosition === null) {
					return
				}
				const limit = 20
				const thisPosition = e.changedTouches[0].clientX
				if (Math.abs(thisPosition - this.touchPosition) > limit) {
					this.changeValueType()
				}
				this.touchPosition = null					
			},
			changeValueType () {
				this.form.value = -1 * this.form.value
			}
		}
	}
</script>

<style lang="scss">
.item-title {
	color: #ccc;
	position: relative;
	text-align: center;
	padding: 10rpx 20rpx;
	font-size: 30rpx;
	&::before {
		content: "";
		position: absolute;
		width: 80rpx;
		height: 2rpx;
		top: 30rpx;
		left: 200rpx;
		background-color: #ccc;
	}
	&::after {
		content: "";
		position: absolute;
		width: 80rpx;
		height: 2rpx;
		top: 30rpx;
		right: 200rpx;
		background-color: #ccc;
	}
}
.value-set {
	width: 100vw;
	display: flex;
	align-items: center;
	justify-content: center;
	.value-in {
		.type {
			color: #F43F3B;
		}
		.value {
			color: #F43F3B;
		}	
	}
	.value-out {
		.type {
			color: #2B85E4;
		}
		.value {
			color: #2B85E4;
		}	
	}
	.value-info {
		display: flex;
		width: 100%;
		// line-height: 40rpx;
		justify-content: center;
		align-items: center;
		position: relative;
		.type {
			position: absolute;
			left: 140rpx;
			width: 100rpx;
			font-size: 40rpx;
		}
		.value {
			font-size: 80rpx;
			font-weight: bolder;
		}
	}
}
.type-set {
	width: 100vw;
	display: flex;
	align-items: center;
	justify-content: center;
	.type-info {
		width: 100%;
		display: flex;
		font-size: 40rpx;
		margin-bottom: 20rpx;
		justify-content: space-around;
		view {
			min-width: 80rpx;
			text-align: center;
			background-color: #fff;
			border: 1rpx solid #ddd;
			padding: 10rpx 40rpx;
			border-radius: 4rpx;
		}
	}
}
.date-set {
	width: 100vw;
	display: flex;
	align-items: center;
	justify-content: center;
	.date-info {
		width: 100%;
		display: flex;
		font-size: 40rpx;
		margin-bottom: 20rpx;
		justify-content: space-around;
		view {
			min-width: 80rpx;
			text-align: center;
			background-color: #fff;
			border: 1rpx solid #ddd;
			padding: 10rpx 40rpx;
			border-radius: 4rpx;
		}
	}
}
.desc-set {
	width: 100vw;
	display: flex;
	align-items: center;
	justify-content: center;
	.desc-info {
		width: 100%;
		display: flex;
		font-size: 40rpx;
		margin-bottom: 20rpx;
		justify-content: space-around;
		textarea {
			border: 2rpx solid #ccc;
			border-radius: 10rpx;
			padding: 16rpx;
		}
	}
}
.set-item {
	height: 180rpx;
}
</style>
