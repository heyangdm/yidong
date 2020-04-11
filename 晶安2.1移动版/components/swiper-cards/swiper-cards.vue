<template>
	<view>
		<scroll-view scroll-x="true" class="tab-h" v-bind:scroll-into-view="scroll_into" v-bind:scroll-with-animation="true">			
			<view v-for="(item, index) in tab_bar" class="tab-item" v-bind:class="current_tab==index ? 'tab-bar-active' : ''" v-bind:key="index" v-bind:data-current="index" v-bind:id="item.id" v-on:click="change_tab">{{item.tit}}</view>
		</scroll-view>
		<view class="hr">
			
		</view>
	</view>
</template>
<script>

	export default {

		data() {
			return {
				// 当前选中tab索引
				current_tab:0,
				// 当前滚动条距离左边的位置
				scroll_left:0,
				// 当前滚动条滚动到id位置
				scroll_into:'',
				// 屏幕宽度
				screen_width:0,
				tab_bar:[
					{
						id : 'emotion',
						tit: '情感'
					},
					{
						id : 'news',
						tit: '新闻'
					},
					{
						id : 'diagrams',
						tit: '八卦'
					},
					{
						id : 'house',
						tit: '楼市'
					},
					{
						id : 'cars',
						tit: '骑车'
					},
					{
						id : 'healthy',
						tit: '健康'
					},
					{
						id : 'workplace',
						tit: '职场'
					},
					{
						id : 'all',
						tit: '全部'
					},
					{
						id : 'other',
						tit: '其他'
					},
					{
						id : 'music',
						tit: '音乐'
					},
					{
						id : 'movie',
						tit: '影视'
					},
					{
						id : 'sport',
						tit: '运动'
					},
					{
						id : 'country',
						tit: '国家'
					}
				]
			}
		},
		onLoad() {
			// 首次获取屏幕宽度
			uni.getSystemInfo({
			    success: (res) =>{
					this.screen_width = res.screenWidth
			    }
			});
		},
		methods: {
			// 点击tabbar事件
			change_tab(e){
				let index = e.target.dataset.current || e.currentTarget.dataset.current;
				// 记录当前点击的选项位置
				this.current_tab = index
				// 如果点击了第4个以后的,滚动条向右移动屏幕的宽度
				this.scroll_into = this.tab_bar[index].id
			}
		}
	}
</script>

<style>

.tab-h {
  height: 80rpx;
  width: 100%;
  line-height: 80rpx;
  background: #f7f7f7;
  font-size: 16px;
  white-space: nowrap;

}
 
.tab-item {
  padding: 0 36rpx;
  display: inline-block;
}
.tab-bar-active{
	font-weight: bold;
	color: #007AFF;
}
.hr{
	height: 1rpx;
	background-color: #eeeeee;
}
</style>