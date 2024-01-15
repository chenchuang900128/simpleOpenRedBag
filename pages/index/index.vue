<template>
	<view class="content">
		<!-- money：红包金额
		show：组件显示隐藏布尔值true/false
		@close：关闭组件回调
		@change：开红包回调 -->
		<cc-packet :money="moneyStr" :show="isShow" @close="close" @change="checkResult">
		</cc-packet>


		<button style="margin-top: 80px;" @click="openRedClick"> 打开红包 </button>
	</view>
</template>

<script>
	import ccPacket from '@/components/cc-packet/cc-packet.vue'
	export default {
		components: {
			ccPacket
		},
		data() {
			return {
				moneyStr: '',
				isShow: false,

			}
		},
		onLoad() {

		},
		methods: {

			// 打开红包
			openRedClick() {

				this.isShow = true;
				this.moneyStr = (Math.random() * 10).toFixed(2);

			},
			// 关闭红包
			close() {
				this.isShow = false;
			},
			checkResult(e) {

				console.log("红包金额 = " + e);
			}
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
</style>