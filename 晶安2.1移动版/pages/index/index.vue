<template>
    <view>
		<!-- 导航 -->
		<uni-nav-bar fixed="true" :background-color="titleBg"  left-icon="back" @click-left="back" @click-right="showMenu" left-text="返回" right-text="菜单" title="首页" backgroundColor="#037ab4" titleColor="#FFFFFF"></uni-nav-bar>
		<!-- 轮播图 -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item>
				<view class="swiper-item"><image src="../../static/banner1.jpg" mode=""></image></view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item"><image src="../../static/banner1.jpg" mode=""></image></view>
			</swiper-item>
		</swiper>
		<!-- 选项卡 -->
<scroll-view scroll-x="true" class="tab-h" v-bind:scroll-into-view="scroll_into" v-bind:scroll-with-animation="true">
			<view v-for="(item, index) in tab_bar" class="tab-item" v-bind:class="current_tab==index ? 'tab-bar-active' : ''"
			 v-bind:key="index" v-bind:data-current="index" v-bind:id="item.id" v-on:click="change_tab">{{item.tit}}</view>
		</scroll-view>
		<view class="hr"></view>
		<swiper class="swiper" v-bind:current="current_tab"  duration="300" @change="change_swiper">
			<swiper-item>
				<view class="swiper-item uni-bg-red">
					<view class="uni-list">
							<view class="uni-list-cell" hover-class="uni-list-cell-hover">
								<view class="uni-media-list">
									<image class="uni-media-list-logo" src="../../static/banner1.jpg"></image>
									<view class="uni-media-list-body">
										<view class="uni-media-list-text-top">产品</view>
										<view class="uni-media-list-text-bottom uni-ellipsis">产品描述：的风格快速到岗</view>
									</view>
								</view>
							</view>
						</view>
				</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-green">B</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-blue">C</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-red">D</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-green">E</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-blue">F</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-red">G</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-green">H</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-blue">I</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-red">J</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-green">K</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-blue">L</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item uni-bg-red">M</view>
			</swiper-item>
		</swiper>
		
	</view>
	
</template>

<script> 
	import uniCard from '@/components/uni-card/uni-card.vue'
    import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
    export default {  
        data() {  
            return {  
             titleBg:'rgba(255,255,255,0)',
			 // 当前选中tab索引
			 // 当前选中tab索引
			 				current_tab: 0,
			 				// 当前滚动条距离左边的位置
			 				scroll_left: 0,
			 				// 当前滚动条滚动到id位置
			 				scroll_into: '',
			 				// 屏幕宽度
			 				screen_width: 0,
			 				tab_bar: [{
			 						id: 'emotion',
			 						tit: '情感'
			 					},
			 					{
			 						id: 'news',
			 						tit: '新闻'
			 					},
			 					{
			 						id: 'diagrams',
			 						tit: '八卦'
			 					},
			 					{
			 						id: 'house',
			 						tit: '楼市'
			 					},
			 					{
			 						id: 'cars',
			 						tit: '骑车'
			 					},
			 					{
			 						id: 'healthy',
			 						tit: '健康'
			 					},
			 					{
			 						id: 'workplace',
			 						tit: '职场'
			 					},
			 					{
			 						id: 'all',
			 						tit: '全部'
			 					},
			 					{
			 						id: 'other',
			 						tit: '其他'
			 					},
			 					{
			 						id: 'music',
			 						tit: '音乐'
			 					},
			 					{
			 						id: 'movie',
			 						tit: '影视'
			 					},
			 					{
			 						id: 'sport',
			 						tit: '运动'
			 					},
			 					{
			 						id: 'country',
			 						tit: '国家'
			 					}
			 				],
			 
			}
		},
        components: {  
            uniNavBar
        },  
        methods: {  
			// 点击tabbar事件
			change_tab(e) {
				let index = e.target.dataset.current || e.currentTarget.dataset.current;
				this.run_tab(index)
			},
			// swiper滑动事件
			change_swiper(e){
				console.log('你啥时候执行啊', e)
				let index = e.target.current || e.detail.current;
				this.run_tab(index)
			},
			// 执行整个tab事件
			run_tab(index){
				// 记录当前滑动的位置
				this.current_tab = index
				// 如果点击了第4个以后的,滚动条向右移动屏幕的宽度
				this.scroll_into = this.tab_bar[index].id
			}
		},  
		onLoad() {
			// 首次获取屏幕宽度
			uni.getSystemInfo({
				success: (res) => {
					this.screen_width = res.screenWidth
				}
			});
		},
        onPageScroll:function(e){  
            this.titleBg = 'rgba(255,255,255,'+e.scrollTop / 300+')';  
        }
		 
    } 
</script>
<style>
	.tab-h {
		height: 80rpx;
		width: 100%;
		line-height: 80rpx;
		background-color: #037ab4;
		font-size: 16px;
		white-space: nowrap;
		color: #FFFFFF;
		padding: 8rpx 2rpx;
		text-align: left;
	}

	.tab-item {
		padding: 0 36rpx;
		display: inline-block;
	}

	.tab-bar-active {
		font-weight: bold;
		background-color: #e68127;
	}

	.hr {
		height: 1rpx;
		background-color: #eeeeee;
	}
	.swiper{
		height: 500rpx;
		text-align: center;
		
	}
	.swiper-item{
		height: 500rpx;
	}
</style>