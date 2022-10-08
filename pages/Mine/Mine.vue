<template>
	<view class="content">
		<view class="head">
			<view class="head_left">
				<view class="head_img">
					<image :src="userHeadImg" mode=""></image>
				</view>
				<view class="userInfo">
					<view class="useName">
						{{userName}}
					</view>
					<view class="userNum">
						{{userPhoneNum}}
					</view>
				</view>

			</view>
			<view class="head_right">
				<image src="../../static/image/setUp.png" mode=""></image>
			</view>
		</view>
		<!-- 常用功能部分 -->
		<view class="mine_common">
			<view class="_title">
				常用功能
			</view>
			<view class="mine_common_tab">
				<view class="_com_list" v-for="(item,index) in commentList" :key="index">
					<view class="_com_list_img">
						<image :src="item.img" mode=""></image>
					</view>
					<view class="_com_list_text">
						{{item.name}}
					</view>
				</view>
			</view>
			<view class="mine_common_tab" style="margin:20rpx 0 0 0">
				<view class="_com_list" v-for="(item,index) in commentListT" :key="index">
					<view class="_com_list_img">
						<image :src="item.img" mode=""></image>
					</view>
					<view class="_com_list_text">
						{{item.name}}
					</view>
				</view>
			</view>
		</view>
		<!-- 更多功能部分 -->
		<view class="mine_more">
			<view class="_title">
				更多功能
			</view>
			<view class="mine_more_tab" style="margin:20rpx 0 0 0">
				<view class="_more_list" v-for="(item,index) in moreList" :key="index">
					<view class="_more_list_img">
						<image :src="item.img" mode=""></image>
					</view>
					<view class="_com_more_text">
						{{item.name}}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default ({
		data() {
			return {
				userHeadImg: 'https://s1.ax1x.com/2022/09/20/xPA5ct.jpg',
				userName: '我的',
				userPhoneNum: '139****6465',
				commentList: [{
						id: 1,
						img: '../../static/image/hetong.png',
						name: '合同'
					},
					{
						id: 2,
						img: '../../static/image/daijiao.png',
						name: '代缴账单'
					}, {
						id: 3,
						img: '../../static/image/youhui.png',
						name: '优惠券'
					}, {
						id: 4,
						img: '../../static/image/qianbao.png',
						name: '我的钱包'
					},

				],
				commentListT: [{
						id: 1,
						img: '../../static/image/wodeshiyou.png',
						name: '我的室友'
					},
					{
						id: 2,
						img: '../../static/image/wodeguanjia.png',
						name: '我的管家'
					}, {
						id: 3,
						img: '../../static/image/wifi.png',
						name: 'WiFi密码'
					}, {
						id: 4,
						img: '../../static/image/sheqvhuodong.png',
						name: '社区活动'
					},
				
				],
				moreList:[{
					id: 1,
					img: '../../static/image/haoping.png',
					name: '给个好评'
				},
				{
					id: 2,
					img: '../../static/image/tousujianyi.png',
					name: '投诉建议'
				},
				{
					id: 3,
					img: '../../static/image/fuwudianhua.png',
					name: '服务电话'
				},
				{id: 4,
					img: '',
					name: ''}]
				

			}
		},
		methods: {

		},
		onload() {

		}
	})
</script>

<style>
	@import url("../../static/css/mine.css");
</style>
