<template>
	<view>
		
		<view class="questionList fs13">
			<view class="item" v-for="(item,index) in mainData" :key="index">
				<view class="flex line">
					<view class="ll"><image class="icon" src="../../static/images/help-icon.png" mode=""></image></view>
					<view class="rr">{{item.title}}</view>
				</view>
				<view class="flex line mgt5">
					<view class="ll"><image class="icon" src="../../static/images/help-icon1.png" mode=""></image></view>
					<view class="rr color6">{{item.description}}</view>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view>没找到问题，咨询客服</view>
				<view @click="Router.redirectTo({route:{path:'/pages/contactKefu/contactKefu'}})"><image class="kefuIcon" src="../../static/images/help-icon2.png" mode=""></image></view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				showView: false,
				wx_info:{},
				is_show:false,
				questionDate:['','','',''],
				mainData:[],
				searchItem:{
					thirdapp_id:2
				}
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			console.log(2323)
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
			getMainData(isNew) {
				const self = this;
				console.log(2323)
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 5
					}
				};
				const postData = {};
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.getBefore = {
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['=', ['帮助与反馈']],
						},
						condition:'in'
					}
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style>
	.questionList .item{padding: 30rpx 4%;border-bottom: 10rpx solid #F5F5F5;}
	.questionList .item .line{align-items: flex-start;}
	.questionList .ll{width: 50rpx;}
	.questionList .ll .icon{width: 28rpx;height: 28rpx;}
	.questionList .rr{width: 92%;}
	
	.kefuIcon{width: 60rpx;height: 54rpx;}
</style>
