<template>
	<view class="content">
		<view class="tabText" v-show='isTopHidding'>
			<view class="_tabs_box" style="width: 100%;margin-top: 0;">
				<u-tabs-swiper ref="uTabs" :list="list" :current="current" @change="tabsChange" :is-scroll="true"
					swiperWidth="750" :show-bar='false'></u-tabs-swiper>
			</view>
		</view>
		<view class="homeNeck">
			<view class="neckTop">
				<view class="selectAdress">
					<view>{{city}}</view>
					<view class="selectDown">
						<image src="../../static/image/selectDown.png"></image>
					</view>
				</view>
				<view class="search">
					<view class="inputBox" @click="LookFor()">
						<view class="inputBox-left">
							<image src="../../static/image/search.png" mode="widthFix"></image>
						</view>

					</view>
				</view>
			</view>
			<!-- 宣传标语 -->
			<view class="neckBottom">
				<view class="slogan">
					<span class="text1">
						新客入住&ensp;品牌公寓</span>
					<span class="text2">真实房源&ensp;专业服务</span>
					<view class="fakeBtn">
						租房首选
					</view>
				</view>

				<view class="inputBg">
					<image src="https://s1.ax1x.com/2022/09/19/x9BLQI.png" mode="scaleToFill"></image>
				</view>
			</view>
		</view>
		<view class="selectServiceBox">
			<view class="selectServiceTitle">
				服务选择
			</view>
			<view class="serviceList">
				<scroll-view scroll-x="true" class="scrollBox">
					<view class="nav-bar-wrap">
						<block v-for="(item, index) in serviceList" :key="index">
							<view class="serviceBox">
								<view class="serviceImgBox">
									<image :src='item.img' mode=""></image>
								</view>
								<view class="serviceName">
									{{item.title}}
								</view>

							</view>
						</block>
					</view>

				</scroll-view>
			</view>
		</view>
		<view style="width: 100%;">
			<view class="_tabs_box" style="width: 100%;" v-show="isTopHidding ==false">
				<u-tabs-swiper ref="uTabs" :list="list" :current="current" @change="tabsChange" :is-scroll="true"
					swiperWidth="750"></u-tabs-swiper>
			</view>
			<swiper :current="swiperCurrent" @transition="transition" @animationfinish="animationfinish">
				<swiper-item class="swiper-item">
					<scroll-view  scroll-y @scrolltolower="onreachBottom">
						<view style="display: flex;flex-wrap: wrap; width: 100%;justify-content: space-around;">
							<view class="homeList" v-for="(item,index) in l_houseInfo" :key="index">
								<view class="home_pic">
									<image :src="item.Image" mode="widthFix">
										<view class="home_text">
											{{item.title}}
										</view>
									</image>
								</view>
								<view class="home_price">
									{{item.price}}
								</view>
								<view class="home_info">
									{{item.speace}}㎡ | {{item.manNum}}居 | {{item.floor}}层
								</view>
								<view class="home_address">
									{{item.address}}
								</view>
							</view>
							
						</view>
						
					</scroll-view>
				</swiper-item>
				<swiper-item class="swiper-item">
					<scroll-view scroll-y @scrolltolower="onreachBottom">
						<view style="display: flex;flex-wrap: wrap; width: 100%;justify-content: space-around;">
							<view class="homeList" v-for="(item,index) in r_houseInfo" :key="index">
								<view class="home_pic">
									<image :src="item.Image" mode="widthFix">
										<view class="home_text">
											{{item.title}}
										</view>
									</image>
								</view>
								<view class="home_price">
									{{item.price}}
								</view>
								<view class="home_info">
									{{item.speace}}㎡ | {{item.manNum}}居 | {{item.floor}}层
								</view>
								<view class="home_address">
									{{item.address}}
								</view>
							</view>
							
						</view>
						
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import QQMapWX from "../../uitl/qqmap-wx-jssdk.js"
	export default {

		data() {
			return {
				address: '',
				title: 'Hello',
				city: '北京',
				isShow: false,
				qqmapsdk: Object,
				scrollTop: 0,
				isTopHidding: false,
				isHidding: true,
				//列表数据
				list: [{
					name: '新上'
				}, {
					name: '附近'
				}],

				// list: [],

				// 因为内部的滑动机制限制，请将tabs组件和swiper组件的current用不同变量赋值
				current: 0, // tabs组件的current值，表示当前活动的tab选项
				swiperCurrent: 0, // swiper组件的current值，表示当前那个swiper-item是活动的

				serviceList: [{
						id: 1,
						title: "整租",
						img: '../../static/image/allHome.png'
					},
					{
						id: 2,
						title: "预约看房",
						img: '../../static/image/yuyue.png',
					},
					{
						id: 3,
						title: "合租",
						img: '../../static/image/danzu.png',
					},
					{
						id: 4,
						title: "水电",
						img: '../../static/image/shuidian.png',
					},
					{
						id: 5,
						title: "独卫",
						img: '../../static/image/duwei.png',
					},
					{
						id: 6,
						title: "添加账单",
						img: '../../static/image/bill.png',
					},
					{
						id: 7,
						title: "公寓",
						img: '../../static/image/flat.png',
					},
					{
						id: 8,
						title: "保洁",
						img: '../../static/image/clean.png',
					},
					{
						id: 9,
						title: "业主委托",
						img: '../../static/image/help.png',
					},
					{
						id: 10,
						title: "公共保修",
						img: '../../static/image/baoxiu.png',
					},
					{
						id: 11,
						title: "账单",
						img: '../../static/image/zhangdan.png',
					},
					{
						id: 12,
						title: "智能门锁",
						img: '../../static/image/mensuo.png',
					},
					{
						id: 13,
						title: "合同",
						img: '../../static/image/contract.png',
					},
					{
						id: 14,
						title: "安全帮助",
						img: '../../static/image/anquan.png',
					},
				],
				l_houseInfo: [{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					}, {
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
				],
				r_houseInfo: [{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					}, {
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},
					{
						Image: 'https://s1.ax1x.com/2022/09/21/xicV9f.jpg',
						title: '这里这里这里......',
						price: 100,
						speace: 30,
						manNum: 2,
						floor: 5,
						address: '历下',
					},

				]
			}

		},
		onLoad() {
			// 进到页面就调用位置授权方法
			this.instantiationAPIClass()
			this.getCoordinate()
		},
		methods: {
			// tabs通知swiper切换
			tabsChange(index) {
				this.swiperCurrent = index;
			},
			// swiper-item左右移动，通知tabs的滑块跟随移动
			transition(e) {
				let dx = e.detail.dx;
				this.$refs.uTabs.setDx(dx);
			},
			// 由于swiper的内部机制问题，快速切换swiper不会触发dx的连续变化，需要在结束时重置状态
			// swiper滑动结束，分别设置tabs和swiper的状态
			animationfinish(e) {
				let current = e.detail.current;
				this.$refs.uTabs.setFinishCurrent(current);
				this.swiperCurrent = current;
				this.current = current;
			},
			// scroll-view到底部加载更多
			onreachBottom() {

			},
			instantiationAPIClass() {
				this.qqmapsdk = new QQMapWX({
					key: 'B3WBZ-JFOCJ-BFRF3-FABHK-HE6DJ-PAFLC'
				})
			},
			// 获取经纬度
			getCoordinate() {
				uni.authorize({
					// 弹窗获取当前地理位置信息
					scope: 'scope.userLocation',
					// 成功时
					success: () => {
						uni.getLocation({
							success: (res) => {
								// 获取位置
								this.getAddress(res.latitude, res.longitude)
							}
						})
					}
				})
			},
			//获取位置
			getAddress(latitude, longitude) {
				this.qqmapsdk.reverseGeocoder({
					// 传坐标
					location: {
						latitude: latitude,
						longitude: longitude
					},
					// 成功回调
					success: (res) => {
						let cityName = res.result.address_component.city
						let reg = /.+?(市)/g;

						this.city = cityName.replace('市', '');
						console.log(this.city);
					}
				})
			},
			//点击input框跳到两一个界面
			LookFor() {
				uni.navigateTo({
					url: "/pages/LookFor/LookFor"
				})
			},
			isChange(i) {
				if (i == 1) {
					this.isShow = false
				} else {
					this.isShow = true
				}

				console.log(this.isShow);
			},
			//获取滚动距离
			onPageScroll: function(e) { //nvue暂不支持滚动监听，可用bindingx代替
				this.scrollTop = e.scrollTop
				// console.log(this.scrollTop);
				if (this.scrollTop >= 410) {
					this.isHidding = false
					this.isTopHidding = true
				} else {
					this.isHidding = true
					this.isTopHidding = false
				}
			},
		}
	}
</script>

<style>
	@import url("../../static/css/homePage.css");
</style>
