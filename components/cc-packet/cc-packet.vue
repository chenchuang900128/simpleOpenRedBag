<template>
	<view v-if="show" class="red-packet">
		<view class="red-packet-layout" :class="open ? 'red-packet-open' : '' ">
			<view class="red-packet-up" />
			<view class="red-packet-middle" />
			<view class="red-packet-content">
				<view class="red-packet-tip">
					<view class="receive-success">
						<view>恭喜您获得了</view>
						<view>
							<text>{{money + ''}}</text>元
						</view>
					</view>
				</view>
			</view>
			<view class="red-packet-top">
				<text>红包来啦</text>
			</view>
			<view v-if="!open" class="open-btn" @click="openClick">開</view>
			<view class="red-packet-bottom"> <text @click="GetClose" v-if="open" class="close">x</text></view>
			<view class="red-packet-left" />
			<view class="red-packet-right" />
			<view class="red-money red-money-left1" />
			<view class="red-money red-money-left2" />
			<view class="red-money red-money-left3" />
			<view class="red-money red-money-left4" />
			<view class="red-money red-money-middle1" />
			<view class="red-money red-money-middle2" />
			<view class="red-money red-money-middle3" />
			<view class="red-money red-money-middle4" />
			<view class="red-money red-money-right1" />
			<view class="red-money red-money-right2" />
			<view class="red-money red-money-right3" />
			<view class="red-money red-money-right4" />
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			//显示/隐藏
			show: {
				type: Boolean,
				default: false
			},
			// 金额
			money: {
				type: [Number, String],
				default: '8.88',
				required: true
			},
		},
		data() {
			return {
				open: false, //状态
				 
			};
		},
		methods: {
			//打开红包
			openClick() {
				this.open = true;
				this.$emit('change', this.money);
			},

			// 关闭红包组件
			GetClose() {
				this.open = false;
				this.$emit('close', false);
			}
		}
	}
</script>

<style lang="scss">
	@keyframes open-top {
		0% {
			transform: rotateX(0);
		}

		100% {
			transform: rotateX(90deg);
		}
	}

	@keyframes open-up {
		0% {
			transform: rotateX(-90deg);
		}

		100% {
			transform: rotateX(0);
		}
	}

	/*红包布局*/
	.red-packet {
		position: fixed;
		top: 0;
		left: 0;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		width: 100vw;
		height: 100vh;
		z-index: 1000;
		background: rgba(0, 0, 0, 0.60);

		.red-packet-layout {
			position: relative;

			.red-packet-open {

				.red-packet-up {
					animation: open-up 0.2s ease-in-out 0.2s 1 normal;
					animation-fill-mode: forwards;
				}
			}

			.red-packet-middle {
				background-color: rgb(209, 64, 64);
				background-size: 490rpx 462rpx;
				border-bottom-left-radius: 20rpx;
				border-bottom-right-radius: 20rpx;
				width: 490rpx;
				height: 462rpx;
			}

			.red-packet-content {
				background-image: url('https://pic.imgdb.cn/item/63101bd416f2c2beb1200613.png');
				background-size: 422rpx 428rpx;
				width: 422rpx;
				height: 428rpx;
				position: absolute;
				top: 84rpx;
				left: 34rpx;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;
			}

		}

		.red-packet-up {
			border-top-left-radius: 250rpx;
			border-top-right-radius: 250rpx;
			background-color: rgb(209, 64, 64);
			background-size: 490rpx 82rpx;
			width: 490rpx;
			height: 82rpx;
			transform: rotateX(-90deg);
			transform-origin: 50% 100%;
		}
	}



	.red-packet .red-packet-layout.red-packet-open .red-packet-content {
		top: -40rpx;
		transition: top 0.2s ease-in-out 0.2s;
	}

	/*打开前头部图*/
	.red-packet .red-packet-layout .red-packet-top {
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 40rpx;
		font-weight: bold;
		color: #fde292;
		background-size: 490rpx 400rpx;
		width: 490rpx;
		height: 400rpx;
		position: absolute;
		top: -55rpx;
		left: 0;
		z-index: 101;
		border-top-left-radius: 20rpx;
		border-top-right-radius: 20rpx;
		background: linear-gradient(rgb(220, 72, 42), rgb(229, 38, 38));
	}

	.close {
		position: absolute;
		text-align: center;
		color: #fff;
		left: 222rpx;
		bottom: -100rpx;
		width: 60rpx;
		height: 60rpx;
		line-height: 50rpx;
		border-radius: 50rpx;
		border: 2rpx solid #fff;
	}


	/*打开按钮*/
	.open-btn {
		display: flex;
		position: absolute;
		justify-content: center;
		align-items: center;
		color: rgb(233, 25, 25);
		font-size: 40rpx;
		top: 300rpx;
		left: 190rpx;
		width: 100rpx;
		height: 100rpx;
		z-index: 104;
		border: 10rpx solid rgb(228, 165, 48);
		border-radius: 50%;
		background-color: rgb(226, 226, 34);
	}

	.red-packet .red-packet-layout.red-packet-open .red-packet-top {
		transform-origin: 0 200rpx;
		animation: open-top 0.2s ease-in-out 0s 1 normal;
		animation-fill-mode: forwards;
	}

	/*打开前底部图片*/
	.red-packet .red-packet-layout .red-packet-bottom {
		background-image: url('https://pic.imgdb.cn/item/63101c9516f2c2beb1206ae6.png');
		background-size: 490rpx 264rpx;
		width: 490rpx;
		height: 264rpx;
		position: absolute;
		top: 278rpx;
		left: 0;
		z-index: 103;
	}



	/*小元宝*/
	.red-packet .red-packet-layout .red-money {
		position: absolute;
		background-image: url("https://pic.imgdb.cn/item/64bdd5dd1ddac507cc18e45b.png");
		visibility: visible;
		transition-property: top;
		transition-duration: 1s;
		transition-timing-function: ease-in-out;
		top: 0;
	}

	.red-packet .red-packet-layout .red-money.red-money-left1 {
		background-size: 44rpx 32rpx;
		width: 44rpx;
		height: 32rpx;
		left: 20rpx;
		transform: rotate(10deg);
		transition-delay: 0.1s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-left1 {
		top: 280rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-left2 {
		background-size: 33rpx 24rpx;
		width: 33rpx;
		height: 24rpx;
		left: 5rpx;
		transform: rotate(20deg);
		transition-delay: 0.2s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-left2 {
		top: 260rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-left3 {
		background-size: 33rpx 24rpx;
		width: 33rpx;
		height: 24rpx;
		left: 60rpx;
		transform: rotate(5deg);
		transition-delay: 0.1s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-left3 {
		top: 300rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-left4 {
		background-size: 33rpx 24rpx;
		width: 33rpx;
		height: 24rpx;
		left: 90rpx;
		transform: rotate(5deg);
		transition-delay: 0.3s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-left4 {
		top: 320rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-middle1 {
		background-size: 90rpx 64rpx;
		width: 90rpx;
		height: 64rpx;
		transition-delay: 0.2s;
		left: 200rpx;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-middle1 {
		top: 320rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-middle2 {
		background-size: 67rpx 48rpx;
		width: 67rpx;
		height: 48rpx;
		left: 160rpx;
		transition-delay: 0.3s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-middle2 {
		top: 322rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-middle3 {
		background-size: 56rpx 40rpx;
		width: 56rpx;
		height: 40rpx;
		left: 120rpx;
		transform: rotate(10deg);
		transition-delay: 0.1s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-middle3 {
		top: 322rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-middle4 {
		background-size: 56rpx 40rpx;
		width: 56rpx;
		height: 40rpx;
		left: 270rpx;
		transition-delay: 0.4s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-middle4 {
		top: 322rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-right1 {
		background-size: 56rpx 40rpx;
		width: 56rpx;
		height: 40rpx;
		right: 50rpx;
		transform: rotate(-30deg);
		transition-delay: 0.2s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-right1 {
		top: 300rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-right2 {
		background-size: 33rpx 24rpx;
		width: 33rpx;
		height: 24rpx;
		right: 26rpx;
		transform: rotate(-10deg);
		transition-delay: 0.3s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-right2 {
		top: 280rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-right3 {
		background-size: 33rpx 24rpx;
		width: 33rpx;
		height: 24rpx;
		right: 0;
		transition-delay: 0.1s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-right3 {
		top: 260rpx;
	}

	.red-packet .red-packet-layout .red-money.red-money-right4 {
		background-size: 44rpx 32rpx;
		width: 44rpx;
		height: 32rpx;
		right: 96rpx;
		transition-delay: 0.2s;
	}

	.red-packet .red-packet-layout.red-packet-open .red-money.red-money-right4 {
		top: 280rpx;
	}

	/*红包*/
	.red-packet .red-packet-layout .red-packet-content .red-packet-tip {
		font-size: 30rpx;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.red-packet .red-packet-layout .red-packet-content .red-packet-tip .receive-success {
		font-size: 35rpx;
		line-height: 100rpx;
		text-align: center;
	}

	.red-packet .red-packet-layout .red-packet-content .red-packet-tip .receive-success text {
		color: red;
		margin-right: 10rpx;
		font-size: 60rpx;
	}
</style>