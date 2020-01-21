<template>
	<view>
		
		<view class="mglr4">
			<view class="personList mgt15">
				<view class="item boxShaow" v-for="(item,index) in mainData" :key="index">
					<view class="picbox">
						<image :data-user_no="item.user_no" 
						@click="Router.navigateTo({route:{path:'/pages/personInfor/personInfor?user_no='+$event.currentTarget.dataset.user_no}})" 
						class="pic" :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image>
						<view class="fixInfor flexRowBetween white fs12">
							<view class="flex">
								<image class="photo" :src="item.headImg" mode=""></image>
								<text>NO.{{item.no}}</text>
							</view>
							<view class="flexEnd" @click="clickGood(index)">
								<image class="xin" :src="item.likeMe.length>0&&item.likeMe[0].status==1?'../../static/images/home-icon2.png':'../../static/images/home-icon1.png'" mode=""></image>
								 <text>{{item.like?item.like.count:0}}</text>
							</view>
						</view>
					</view>
					<view class="pdlr4 infor pdb15 color6">
						<view class="flexRowBetween titBox pdb10 pdt15">
							<view class="flex fs14 ll">
								<text>{{item.name}}</text>
								<text class="mgl10 mgr10">{{item.city}}·{{item.country}}</text>
								<text class="mgr10">{{item.age}}岁</text>
								<text>{{item.marriage}}</text>
							</view>
							<view class="rr flexEnd fs12 color9" @click="">
								<image class="seeIcon" src="../../static/images/home-icon3.png" mode=""></image>
								<text>{{item.view_count}}</text>
							</view>
						</view>
						<view class="fs13 avoidOverflow2">{{item.introduction}}</view>
					</view>
					
				</view>
			</view>
			
		</view>
		
		
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,

				personDate: [{},{}],
				mainData:[]
			}
		},
		
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
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
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
				   thirdapp_id:2,
				   user_type:0
				};
				postData.getBefore = {
					test: {
						tableName: 'Log',
						searchItem: {
							status:['in',[1]],
							type:['in',[1]],
							user_no:['in',[uni.getStorageSync('user_info').user_no]]
						},
						middleKey: 'user_no',
						key: 'relation_user',
						condition: 'in',
					},
				};
				postData.getAfter = {
					likeMe: {
						tableName: 'Log',
						searchItem: {
							status:['in',[1,-1]],
							type:1,
							user_no:wx.getStorageSync('user_info').user_no
						},
						middleKey: 'user_no',
						key: 'relation_user',
						condition: 'in',
					},
					like: {
						tableName: 'Log',
						searchItem: {
							status:1,
							type:1,
						},
						middleKey: 'user_no',
						key: 'relation_user',
						condition: 'in',
						compute:{
						  count:[
						    'count',
						    'count',
						    {
						      status:1,
						    }
						  ]
						},
					},
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data)
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			clickGood(index) {
				const self = this;
				uni.setStorageSync('canClick', false);	
				if (self.mainData[index].likeMe.length == 0) {
					self.addGoodLog(index)
				} else {
					self.updateGoodLog(index)
				};
			},
			
			addGoodLog(index) {
				const self = this;
				const postData = {};
				postData.data = {
					type: 1,
					title: '收藏成功',
					relation_user: self.mainData[index].user_no,
					relation_table:'UserInfo',
					user_no: uni.getStorageSync('user_info').user_no,
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.solely_code == 100000) {
						self.mainData[index].likeMe.push({
							status: 1,
							id: res.info.id
						});
						self.mainData[index].like.count = self.mainData[index].like.count+1
						self.$Utils.showToast('已收藏', 'none', 1000)
					} else {
						self.$Utils.showToast('收藏失败', 'none', 1000)
					};
					uni.setStorageSync('canClick', true);	
				};
				self.$apis.logAdd(postData, callback);
			},
			
			
			updateGoodLog(index) {
				const self = this;
			
				const postData = {
					searchItem: {
						id: self.mainData[index].likeMe[0].id
						
					},
					data: {
						status: -self.mainData[index].likeMe[0].status
					}
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					uni.setStorageSync('canClick', true);
					if (res.solely_code == 100000) {
						self.mainData[index].likeMe[0].status = -self.mainData[index].likeMe[0].status;
						if(self.mainData[index].likeMe[0].status==1){
							self.mainData[index].like.count = self.mainData[index].like.count+1
							self.$Utils.showToast('已收藏', 'none', 1000)
						}else{
							
							self.$Utils.showToast('取消成功', 'none', 1000);
							setTimeout(function() {
								self.getMainData(true)
							}, 1000);
						}
					} else {
						self.$Utils.showToast(res.msg, 'none', 1000)
					};
				};
				self.$apis.logUpdate(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/personList.css";
	

</style>
