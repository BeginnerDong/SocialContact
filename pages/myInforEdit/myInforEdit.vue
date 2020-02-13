<template>
	<view>
		
		<view class="pdlr4 myInforEdit mgt15">
			<view class="item">
				<view class="tit">你的姓名？</view>
				<view class="flexRowBetween fs12">
					<view class="text">可填写昵称！</view>
					<view class="flexEnd rr">
						<input type="text" v-model="submitData.name" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的出生年月？</view>
				<view class="flexRowBetween fs12">
					<view class="text">会推算您的年龄噢！</view>
					<view class="flexEnd rr">
						
						<picker mode="date"  @change="birthdayChange">
							<view>{{submitData.birthday!=''?submitData.birthday:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的星座？</view>
				<view class="flexRowBetween fs12">
					<view class="text">看哪个星座和你更匹配</view>
					<view class="flexEnd rr">
						<picker mode="selector" :range="constellationData"  @change="Change" data-key="constellation">
							<view>{{constellationData[constellationIndex]?constellationData[constellationIndex]:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的身高？</view>
				<view class="flexRowBetween fs12">
					<view class="text">异性有时候看重身高</view>
					<view class="flexEnd rr">
						<picker mode="selector" value="28" :range="heightData" @change="Change" data-key="height">
							<view>{{heightData[heightIndex]?heightData[heightIndex]:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">你的体重？</view>
				<view class="flexRowBetween fs12">
					<view class="text">异性有时候很在意体重</view>
					<view class="flexEnd rr">
						<picker mode="selector" value="28" :range="weightData" @change="Change" data-key="weight">
							<view>{{weightData[weightIndex]?weightData[weightIndex]:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的学历？</view>
				<view class="flexRowBetween fs12">
					<view class="text">更好的展示自己</view>
					<view class="flexEnd rr">
						<picker mode="selector" :range="educationData"  @change="Change" data-key="education">
							<view>{{educationData[educationIndex]?educationData[educationIndex]:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">婚姻状况？</view>
				<view class="flexRowBetween fs12">
					<view class="text">严格审核婚姻，酒托</view>
					<view class="flexEnd rr">
						<picker mode="selector" :range="marriageData"  @change="Change" data-key="marriage">
							<view>{{marriageData[marriageIndex]?marriageData[marriageIndex]:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的籍贯？</view>
				<view class="flexRowBetween fs12">
					<view class="text">三百年前是一家</view>
					<view class="flexEnd rr">
						<picker mode="region"  @change="hometownChange">
							<view>{{submitData.hometown!=''?submitData.hometown:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你工作生活在？</view>
				<view class="flexRowBetween fs12">
					<view class="text">可以一起约个饭</view>
					<view class="flexEnd rr">
						<picker mode="region"  @change="addressChange">
							<view>{{submitData.province!=''?submitData.province:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的职业？</view>
				<view class="flexRowBetween fs12">
					<view class="text">异性有时很在乎职业</view>
					<view class="flexEnd rr">
						<picker mode="selector" :range="occupationData"  @change="Change" data-key="occupation">
							<view>{{occupationData[occupationIndex]?occupationData[occupationIndex]:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的微信？</view>
				<view class="flexRowBetween fs12">
					<view class="text">方便心动的TA联系你</view>
					<view class="flexEnd rr">
						<input type="text" v-model="submitData.wechat" />
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的手机号？</view>
				<view class="flexRowBetween fs12">
					<view class="text">方便心动的TA联系你</view>
					<view class="flexEnd rr">
						<input type="number" v-model="submitData.phone" maxlength="11"/>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">你的月收入？</view>
				<view class="flexRowBetween fs12">
					<view class="text">其实人品更重要</view>
					<view class="flexEnd rr">
						<picker mode="selector" :range="salaryData"  @change="Change" data-key="salary">
							<view>{{salaryData[salaryIndex]?salaryData[salaryIndex]:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">房车情况？</view>
				<view class="flexRowBetween fs12">
					<view class="text">更好的找到那个TA</view>
					<view class="flexEnd rr">
						<picker mode="selector" :range="assetsData"  @change="Change" data-key="assets">
							<view>{{assetsData[assetsIndex]?assetsData[assetsIndex]:'请选择'}}</view>
						</picker>
						<image class="arrowR" src="../../static/images/data-icon8.png" mode=""></image>
					</view>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">你的兴趣爱好？<text class="fs12 color9">让那个TA更好的了解你</text></view>
				<view class="likeLable flex fs12 color6">
					<view class="btn"  @click="checkLike(item)" 
					v-for="(item,index) in likeLable" :class="Utils.inArray(item,chooseLike)!=-1?'on':''" 
					:key="index">{{item}}</view>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">个人介绍<text class="fs12 color9 mgl5">让那个TA更了解你</text></view>
				<view class="fs12 color6 mgt10">
					<textarea class="f5bj radius10" style="height: 200rpx;" v-model="submitData.introduction" placeholder="请输入" placeholder-class="placeholder"/>
				</view>
			</view>
			
			<view class="item">
				<view class="tit">择偶标准<text class="fs12 color9 mgl5">更好的找到那个TA</text></view>
				<view class="fs12 color6 mgt10">
					<textarea class="f5bj radius10" style="height: 200rpx;" v-model="submitData.spouse_standard" placeholder="请输入" placeholder-class="placeholder"/>
				</view>
			</view>
			<view class="item">
				<view class="tit">封面<text class="fs13 mgl10"></text></view>
				<view class="fs12 color6 mgt10 upPhoto flex mgt10">
					<view class="lis"  v-for="item in submitData.mainImg" style="position: relative;">
						<image :src="item.url" mode=""></image>
						<image @click="deleteImg(index,'1')" src="../../static/images/deleteImg.png" mode="" style="width: 35rpx;height: 35rpx;position: absolute;top: -17.5rpx;right:-17.5rpx;"></image>
					</view>
					<view class="lis" v-if="submitData.mainImg.length<9" @click="upLoadImg('mainImg')">
						<image src="../../static/images/data-icon9.png" mode=""></image>
						
					</view>
				</view>
			</view>
			<view class="item">
				<view class="tit">相册<text class="fs13 mgl10">(可上传多张,最多6张)</text></view>
				<view class="fs12 color6 mgt10 upPhoto flex mgt10">
					<view class="lis"  v-for="item in submitData.bannerImg" style="position: relative;">
						<image :src="item.url" mode=""></image>
						<image @click="deleteImg(index,'2')" src="../../static/images/deleteImg.png" mode="" 
						style="width: 35rpx;height: 35rpx;position: absolute;top: -17.5rpx;right:-17.5rpx;"></image>
					</view>
					<view class="lis" v-if="submitData.bannerImg.length<9" @click="upLoadImg('bannerImg')">
						<image src="../../static/images/data-icon9.png" mode=""></image>
					</view>
				</view>
			</view>
			
		</view>
		
		<view class="submitbtn pdtb25">
			<button class="btn" type="button" open-type="getUserInfo" @getuserinfo="Utils.stopMultiClick(submit)">确定</button>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				likeLable:[
					
				],
				submitData:{
					name:'',
					gender:'',
					phone:'',
					mainImg:[],
					
					bannerImg:[],
					wechat:'',
					age:'',
					birthday:'',
					height:'',
					constellation:'',
					weight:'',
					occupation:'',
					salary:'',
					education:'',
					marriage:'',
					hometown:'',
					province:'',
					city:'',
					country:'',
					hobby:'',
					assets:'',
					introduction:'',
					spouse_standard:''
				},
				constellationData:['白羊座','金牛座','双子座','巨蟹座','狮子座','处女座','天秤座','天蝎座','射手座','摩羯座','水瓶座','双鱼座'],
				constellationIndex:-1,
				heightData:[],
				heightIndex:-1,
				weightData:[],
				weightIndex:-1,
				educationData:['高中及高中以下','大专','本科','研究生及研究生以上'],
				educationIndex:-1,
				marriageData:['未婚','已婚'],
				marriageIndex:-1,
				occupationData:['学生','销售','IT/互联网','通信/电子','生产/制造','物流/仓储','商贸/仓储','人事/行政',
				'高级管理','广告/市场','传媒/艺术','生物/制药','医疗/护理','金融','建筑/房地产','咨询/顾问','法律',
				'财会/审计','教育/科研','服务业','交通运输','政府机构','军人/警察','农林牧渔','自由职业','待业','其他'],
				occupationIndex:-1,
				salaryData:['2K-3K','3K-5K','5K-1W','1W以上'],
				salaryIndex:-1,
				assetsData:['有房无车','有车无房','有车有房','无车无房'],
				assetsIndex:-1,
				chooseLike:[],
			}
		},
		
		onLoad(options) {
			const self = this;
			for(var i=140;i<221;i++){
				self.heightData.push(i+'cm');
			}
			console.log(self.heightData);
			for(var i=40;i<100;i++){
				self.weightData.push(i+'kg');
			};
			if(options.gender){
				self.submitData.gender = options.gender
			};
			self.likeLable = uni.getStorageSync('user_info').thirdApp.hobby.split(',');
			if(options.gender){
				self.submitData.gender = options.gender
			}
			console.log(self.submitData.gender)
			if(self.heightData.length>0&&self.weightData.length){
				self.$Utils.loadAll(['getMainData'], self);
			}
			
		},
		
		methods: {
			
			deleteImg(index,type){
				const self = this;
				if(type=='1'){
					self.submitData.mainImg.splice(parseInt(index), 1);
				}else{
					self.submitData.bannerImg.splice(parseInt(index), 1);
				}	
			},
			
			submit() {
				const self = this;
				
				uni.setStorageSync('canClick', false);
				const pass = self.$Utils.checkComplete(self.submitData);
				console.log('pass', pass);
				console.log('self.submitData',self.submitData)
				
				if (pass) {	
					const callback = (user, res) => {
						console.log(res)
						self.userInfoUpdate();
					};
					self.$Utils.getAuthSetting(callback);
	
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				};
			},
			
			changeSex(currSex){
				const self = this;
				if(currSex!=self.currSex){
					self.currSex = currSex;
					self.submitData.gender = self.currSex
				}
			},
			
			upLoadImg(type) {
				const self = this;	
				if (self.submitData[type].length > 5) {
					api.showToast('仅限6张', 'fail');
					return;
				};
				wx.showLoading({
					mask: true,
					title: '上传中',
				});
				const callback = (res) => {
					console.log('res', res)
					if (res.solely_code == 100000) {
						self.submitData[type].push({url:res.info.url,type:'image'})
						console.log('type',type)
						console.log(self.submitData)
						wx.hideLoading()
					} else {
						self.$Utils.showToast('网络故障', 'none')
					}
				};				
				wx.chooseImage({
					count: 9,
					success: function(res) {
						console.log(res);
						var tempFilePaths = res.tempFilePaths;
						console.log(callback)
						for (var i = 0; i < tempFilePaths.length; i++) {
							self.$Utils.uploadFile(tempFilePaths[i], 'file', {
								tokenFuncName: 'getProjectToken'
							}, callback)
						}
					},
					fail: function(err) {
						wx.hideLoading();
					},			
				})			
			},
			
			userInfoUpdate() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('完善成功', 'none', 1000)
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
						
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.userInfoUpdate(postData, callback);
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						self.submitData.name = self.mainData.name;
						if(self.submitData.gender==''){
							self.submitData.gender = self.mainData.gender;
						};
						self.submitData.phone = self.mainData.phone;
						self.submitData.mainImg = self.mainData.mainImg;
						self.submitData.bannerImg = self.mainData.bannerImg;
						self.submitData.wechat = self.mainData.wechat;
						self.submitData.age = self.mainData.age;
						self.submitData.birthday = self.mainData.birthday;
						self.submitData.hometown = self.mainData.hometown;
						self.submitData.province = self.mainData.province;
						self.submitData.city = self.mainData.city;
						self.submitData.country = self.mainData.country;
						self.submitData.introduction = self.mainData.introduction;
						self.submitData.spouse_standard = self.mainData.spouse_standard;
						self.submitData.hobby = self.mainData.hobby;
						if(self.mainData.hobby!=''){
							self.chooseLike = self.submitData.hobby.split(',');
						};
						
						for (var i = 0; i < self.heightData.length; i++) {
							if(self.heightData[i]==self.mainData.height){
								self.heightIndex =i
								self.submitData.height = self.mainData.height
							}
						};
						for (var i = 0; i < self.constellationData.length; i++) {
							if(self.constellationData[i]==self.mainData.constellation){
								self.constellationIndex =i
								self.submitData.constellation = self.mainData.constellation
							}
						};
						for (var i = 0; i < self.weightData.length; i++) {
							if(self.weightData[i]==self.mainData.weight){
								self.weightIndex =i
								self.submitData.weight = self.mainData.weight
							}
						};
						for (var i = 0; i < self.occupationData.length; i++) {
							if(self.occupationData[i]==self.mainData.occupation){
								self.occupationIndex =i
								self.submitData.occupation = self.mainData.occupation
							}
						};
						for (var i = 0; i < self.salaryData.length; i++) {
							if(self.salaryData[i]==self.mainData.salary){
								self.salaryIndex =i
								self.submitData.salary = self.mainData.salary
							}
						};
						for (var i = 0; i < self.occupationData.length; i++) {
							if(self.occupationData[i]==self.mainData.occupation){
								self.occupationIndex =i
								self.submitData.occupation = self.mainData.occupation
							}
						};
						for (var i = 0; i < self.salaryData.length; i++) {
							if(self.salaryData[i]==self.mainData.salary){
								self.salaryIndex =i
								self.submitData.salary = self.mainData.salary
							}
						};
						for (var i = 0; i < self.educationData.length; i++) {
							if(self.educationData[i]==self.mainData.education){
								self.educationIndex =i
								self.submitData.education = self.mainData.education
							}
						};
						for (var i = 0; i < self.marriageData.length; i++) {
							if(self.marriageData[i]==self.mainData.marriage){
								self.marriageIndex =i
								self.submitData.marriage = self.mainData.marriage
							}
						};
						for (var i = 0; i < self.assetsData.length; i++) {
							if(self.assetsData[i]==self.mainData.assets){
								self.assetsIndex =i
								self.submitData.assets = self.mainData.assets
							}
						};
					}
					console.log('self.mainData', self.mainData)
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			
			birthdayChange(e){
				const self = this;
				self.submitData.birthday = e.detail.value;
				self.submitData.age = new Date().getFullYear()-parseInt(self.submitData.birthday.split('-')[0])
				console.log(self.submitData);
			},
			
			Change(e){
				const self = this;
				self[e.currentTarget.dataset.key+'Index'] = e.detail.value;
				self.submitData[e.currentTarget.dataset.key] = self[e.currentTarget.dataset.key+'Data'][e.detail.value];
				console.log(self.submitData);
			},
			
			hometownChange(e){
				const self =  this;
				self.submitData.hometown = e.detail.value[0]+e.detail.value[1]+e.detail.value[2];
				console.log(e);
			},
			
			addressChange(e){
				const self =  this;
				self.submitData.province = e.detail.value[0];
				self.submitData.city  = e.detail.value[1];
				self.submitData.country = e.detail.value[2];
				console.log(e);
			},
			
			
			checkLike(item) {
				const self = this;
				console.log('self.chooseLike',self.chooseLike)
				var position = self.chooseLike.indexOf(item);
				console.log('self.chooseLike',self.chooseLike)
				if (position >= 0) {
					self.chooseLike.splice(position, 1);
				} else {
					self.chooseLike.push(item);
				};
				self.submitData.hobby = self.chooseLike.join(',')
				
				console.log('self.chooseLike',self.chooseLike)
				console.log('self.submitData.hobby',self.submitData.hobby)
			},

		}
	};
</script>

<style>
	.myInforEdit .item{padding: 30rpx 4%;border-radius: 10rpx;box-shadow: 0 0 10rpx rgba(0,0,0,0.1);background: #FFF;margin-bottom: 30rpx;}
	.myInforEdit .item .tit{font-size:30rpx; margin-bottom: 10rpx;}
	.myInforEdit .item .text{width: 40%;color: #999;}
	.myInforEdit .item .rr{border-bottom: 1px solid #0A6B67;padding-bottom: 4rpx;padding: 0 10rpx;box-sizing: border-box;padding-bottom: 4rpx;}
	.myInforEdit .item .rr input{width: 100%;line-height: 20rpx;display: block;text-align: right;padding: 0 10rpx;box-sizing: border-box;font-size: 24rpx;color: #666;}
	
	.likeLable{flex-wrap: wrap;}
	.likeLable .btn{min-width: 140rpx;text-align: center;line-height: 50rpx;border-radius: 30rpx;border:1px solid #cdcdcd;box-sizing: border-box;padding: 0 30rpx;margin-right:22rpx; margin-top: 30rpx;}
	.likeLable .btn:nth-of-type(4n){margin-right: 0;}
	.likeLable .btn.on{background: #0A6B67;color: #fff;border-color:#0A6B67;}
	
	.upPhoto{flex-wrap: wrap;}
	.upPhoto .lis{width:200rpx;height: 140rpx;margin:0 16rpx 16rpx 0;}
	.upPhoto .lis image{width: 100%;height: 100%;}
	.upPhoto .lis:nth-of-type(3n){margin-right: 0;}
</style>
