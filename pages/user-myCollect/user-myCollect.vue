<template>
	<view>
		
		<view class="mglr4">
			<view class="personList mgt15">
				<view class="item boxShaow" v-for="(item,index) in personDate" :key="index">
					<view class="picbox" @click="Router.navigateTo({route:{path:'/pages/personInfor/personInfor'}})">
						<image class="pic" src="../../static/images/home-img.png" mode=""></image>
						<view class="fixInfor flexRowBetween white fs12">
							<view class="flex">
								<image class="photo" src="../../static/images/user-icon.png" mode=""></image>
								<text>NO.1025</text>
							</view>
							<view class="flexEnd">
								<image class="xin" src="../../static/images/home-icon1.png" mode=""></image>
								<text>4</text>
							</view>
						</view>
					</view>
					<view class="pdlr4 infor pdb15 color6">
						<view class="flexRowBetween titBox pdb10 pdt15">
							<view class="flex fs14 ll">
								<text>张三</text>
								<text class="mgl10 mgr10">西安市·雁塔区</text>
								<text class="mgr10">1989年</text>
								<text>未婚</text>
							</view>
						</view>
						<view class="fs13 avoidOverflow2">法规及是反过来胡椒粉第三轮后方可大是否会回访近肯定是开发孵化基地</view>
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
				showView: false,
				wx_info:{},
				is_show:false,
				personDate: [{},{}]
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>

<style>
	@import "../../assets/style/personList.css";
	

</style>
