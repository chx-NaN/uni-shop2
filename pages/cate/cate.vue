<template>
	<view>
		<!-- 分类导航区域 -->
		<view class="nav-list">
			<view class="nav-item" v-for="(item, i) in navList" :key="i">
				<image :src="item.image_src" class="nav-img"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				//1. 分类导航的数据列表
				navList: [],
			};
		},
		onLoad() {
			// 2. 在 onLoad 中调用获取数据的方法
			this.getNavList()
		},
		methods: {
			// 3. 在 methods 中定义获取数据的方法
			async getNavList() {
				const { data: res } = await uni.$http.get('/api/public/v1/home/catitems')
				if (res.meta.status !== 200) return uni.$showMsg()
				this.navList = res.message
			},
		}
	}
</script>

<style lang="scss">
	.nav-list {
	display: flex;
	justify-content: space-around;
	margin: 15px 0;
	.nav-img {
	width: 128rpx;
	height: 140rpx;
	}
	}
</style>
