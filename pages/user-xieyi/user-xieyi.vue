<template>
	<view>
		
		<view class="mglr4">
			<view class="fs14 center pdt20 pdb10">{{mainData.title}}</view>
			<view class="xqInfor fs12">
				<view class="content ql-editor" style="padding:0;"
				v-html="mainData.content">
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
				mainData:{}
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.getBefore = {
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['=', ['用户协议']],
						},
						condition:'in'
					}
				};
				postData.searchItem = {
					thirdapp_id:2
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	.xqInfor view{margin-bottom: 10rpx;}
</style>
