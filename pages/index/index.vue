<template>
	<view class="index">
		<view class="nav-bar-userset">
			<view class="nav-bar-userset-add"></view>
			<image src="/static/logo.png" class="nav-bar-userset-logo"></image>
			<image src="/static/add.png" class="nav-bar-userset-add" @tap="addNewSchedule"></image>
		</view>
		<swiper :style="{ height: scrollHeight }" :indicator-dots="swiper.indicatorDots" :duration="swiper.duration">
			<swiper-item>
				<scroll-view class="main-view" scroll-y="true" :style="{ height: scrollHeight }">
					<view class="date-view" 
							v-for="(item, index) in itemProperty" 
							:key="index" 
							>
						<view class="time-process-block" :style="{ backgroundColor: item.backgroundColor }">
							<view class="top-line" @tap="changeDetailShow" :data-id="index">
								<view class="red-point"></view>
								<view class="time-name">{{item.title}}</view>
								<view class="precess-percent">{{ item.process }}%</view>
							</view>
							<view class="all-process" @tap="changeDetailShow" :data-id="index">
								<view class="little-person" :animation="item.animationDataPerson">
									<view class="chat-frame">
										<view class=".chat-frame-content">{{item.now}}</view>
										<image src="/static/chat-frame.png" class="chat-frame-image"></image>
									</view>
									<image src="/static/little-person.png" class="little-person-image"/>
								</view>
								<view class="process-bar">
									<view class="start-text">{{item.start}}</view>
									<view class="blank-bar"></view>
									<view class="end-text">{{item.end}}</view>
									<view class="finish-bar" :animation="item.animationDataProcess"></view>
								</view>
							</view>
						</view>
						<view 
							:style="{ backgroundColor: item.backgroundColor, animation: item.showAnimation}"
							:class="{'schedule-detail-show': item.itemDetail ,'schedule-detail-hidden': !item.itemDetail}"
							ref="scheduleDetail"
							scroll-y="true">
							<view class="detail-contain">
							<scroll-view scroll-y="true" class="all-tag-view">
								<view class="tag-view-up">
									<view class="detail-title-item">
										<view class='detail-title-item-text'>小任务</view>
									</view>
									<view class="tag-view" 
										:style="{ backgroundColor: tag.nowTagColor , color: tag.fontColor}" 
										@tap="setColor" 
										:data-id="index"
										:data-tagid="tagIndex"
										v-for="(tag, tagIndex) in item.tagItems" 
										:key="tagIndex">
										{{ tag.name }}
									</view>
								</view>
							</scroll-view>
							<scroll-view scroll-y="true" class="detail-note">
								<view class="detail-title-item">
									<view class='detail-title-item-text'>备忘录</view>
								</view>
								<view class="detail-note-text" :style="{backgroundColor: item.tagColor}">
									{{item.detailNote}}
								</view>
							</scroll-view>
							</view>
						</view>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<memo></memo>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	import memo from "@/components/memo.vue"
	export default {
		components:{
			memo
		},
		data() {
			return {
				swiper:{
					indicatorDots: false,
					autoplay: false,
					duration: 300
				},
				
				unit: "upx",
				scrollHeight: "",
				itemProperty:[
					{
						index: 0,
						title: "今天",
						process: 60,
						start: "00",
						end: "24",
						now: "16:30",
						backgroundColor: "rgb(171,216,200)",
						animationDataProcess: "",
						animationDataPerson: "",
						tagColor: "rgb(151,196,180)",
						itemDetail: false,
						tagAnimation: "",
						showAnimation: "",
						detailNote: "暂无备忘内容",
						tagItems:[
							{
								name: "大学物理学",
								weight: 10,
								nowTagColor: "",
								fontColor: ""
							},
							{
								name: "大学英语",
								weight: 15,
								nowTagColor: "",
								fontColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: "",
								fontColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: "",
								fontColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: "",
								fontColor: ""
							},
							{
								name: "模拟电路",
								weight: 20,
								nowTagColor: "",
								fontColor: ""
							},
							{
								name: "数字电路",
								weight: 18,
								nowTagColor: "",
								fontColor: ""
							},
						]
					},
					{
						index: 1,
						title: "减肥",
						process: 85,
						start: "00",
						end: "24",
						now: "16:30",
						backgroundColor: "rgb(200,220,200)",
						animationDataProcess: "",
						animationDataPerson: "",
						tagColor: "rgb(180,200,180)",
						itemDetail: false,
						tagAnimation: "",
						showAnimation: "",
						detailNote: "暂无备忘内容",
						tagItems:[
							{
								name: "大学物理学",
								weight: 10,
								nowTagColor: ""
							},
							{
								name: "大学英语",
								weight: 15,
								nowTagColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: ""
							},
							{
								name: "模拟电路",
								weight: 20,
								nowTagColor: ""
							},
							{
								name: "数字电路",
								weight: 18,
								nowTagColor: ""
							},
						]
					},
					{
						index: 2,
						title: "今年",
						process: 42,
						start: "00",
						end: "24",
						now: "16:30",
						backgroundColor: "rgb(235,235,190)",
						animationDataProcess: "",
						animationDataPerson: "",
						tagColor: "rgb(215,215,170)",
						itemDetail: false,
						tagAnimation: "",
						showAnimation: "",
						detailNote: "暂无备忘内容",
						tagItems:[
							{
								name: "大学物理学",
								weight: 10,
								nowTagColor: ""
							},
							{
								name: "大学英语",
								weight: 15,
								nowTagColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: ""
							},
							{
								name: "模拟电路",
								weight: 20,
								nowTagColor: ""
							},
							{
								name: "数字电路",
								weight: 18,
								nowTagColor: ""
							},
						]
					},
					{
						index: 3,
						title: "本周",
						process: 5,
						start: "00",
						end: "24",
						now: "16:30",
						backgroundColor: "rgb(254,225,160)",
						animationDataProcess: "",
						animationDataPerson: "",
						tagColor: "rgb(234,205,140)",
						itemDetail: false,
						tagAnimation: "",
						showAnimation: "",
						detailNote: "暂无备忘内容",
						tagItems:[
							{
								name: "大学物理学",
								weight: 10,
								nowTagColor: ""
							},
							{
								name: "大学英语",
								weight: 15,
								nowTagColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: ""
							},
							{
								name: "模拟电路",
								weight: 20,
								nowTagColor: ""
							},
							{
								name: "数字电路",
								weight: 18,
								nowTagColor: ""
							},
						]
					},
					{
						index: 4,
						title: "英语",
						process: 18,
						start: "00",
						end: "24",
						now: "16:30",
						backgroundColor: "rgb(247,211,126)",
						animationDataProcess: "",
						animationDataPerson: "",
						tagColor: "rgb(227,191,106)",
						itemDetail: false,
						tagAnimation: "",
						showAnimation: "",
						detailNote: "暂无备忘内容",
						tagItems:[
							{
								name: "大学物理学",
								weight: 10,
								nowTagColor: ""
							},
							{
								name: "大学英语",
								weight: 15,
								tagColor: "rgb(246,215,32)",
								nowTagColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: ""
							},
							{
								name: "模拟电路",
								weight: 20,
								nowTagColor: ""
							},
							{
								name: "数字电路",
								weight: 18,
								nowTagColor: ""
							},
						]
					},
					{
						index: 5,
						title: "追剧",
						process: 91,
						start: "00",
						end: "24",
						now: "16:30",
						backgroundColor: "rgb(243,243,173)",
						animationDataProcess: "",
						animationDataPerson: "",
						tagColor: "rgb(223,223,153)",
						itemDetail: false,
						tagAnimation: "",
						showAnimation: "",
						detailNote: "暂无备忘内容",
						tagItems:[
							{
								name: "大学物理学",
								weight: 10,
								nowTagColor: ""
							},
							{
								name: "大学英语",
								weight: 15,
								nowTagColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: ""
							},
							{
								name: "模拟电路",
								weight: 20,
								nowTagColor: ""
							},
							{
								name: "数字电路",
								weight: 18,
								nowTagColor: ""
							},
						]
					},
					{
						index: 6,
						title: "大物",
						process: 99,
						start: "00",
						end: "24",
						now: "16:30",
						backgroundColor: "rgb(186,233,220)",
						animationDataProcess: "",
						animationDataPerson: "",
						tagColor: "rgb(166,213,200)",
						itemDetail: false,
						tagAnimation: "",
						showAnimation: "",
						detailNote: "暂无备忘内容",
						tagItems:[
							{
								name: "大学物理学",
								weight: 10,
								nowTagColor: ""
							},
							{
								name: "大学英语",
								weight: 15,
								nowTagColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: ""
							},
							{
								name: "模拟电路",
								weight: 20,
								nowTagColor: ""
							},
							{
								name: "数字电路",
								weight: 18,
								nowTagColor: ""
							},
						]
					},
					{
						index: 7,
						title: "弹琴",
						process: 86,
						start: "00",
						end: "24",
						now: "16:30",
						backgroundColor: "rgb(174,187,234)",
						animationDataProcess: "",
						animationDataPerson: "",
						tagColor: "rgb(154,167,214)",
						itemDetail: false,
						tagAnimation: "",
						showAnimation: "",
						detailNote: "暂无备忘内容",
						tagItems:[
							{
								name: "大学物理学",
								weight: 10,
								nowTagColor: ""
							},
							{
								name: "大学英语",
								weight: 15,
								nowTagColor: ""
							},
							{
								name: "计算机引论",
								weight: 18,
								nowTagColor: ""
							},
							{
								name: "模拟电路",
								weight: 20,
								nowTagColor: ""
							},
							{
								name: "数字电路",
								weight: 18,
								nowTagColor: ""
							},
						]
					}
				]
			};
		},
		onLoad() {
			this.scrollHeight = uni.getSystemInfoSync().windowHeight + 10 + "px";
			this.pixelRatio = uni.getSystemInfoSync().pixelRatio;
		},
		onReady() {
			var animation = uni.createAnimation({
				delay: 300,
				duration: 500,
				timingFunction: 'ease',
			})
			for (var i = 0; i < this.itemProperty.length ;  i++) {
				this.itemProperty[i].animationDataProcess = animation.translateX(this.itemProperty[i].process*1.5)
														.scaleX(this.itemProperty[i].process*3)
														.step()
														.export()
			}
			animation = uni.createAnimation({
				delay: 300,
				duration: 500,
				timingFunction: 'ease',
			})
			for (var i = 0; i < this.itemProperty.length ;  i++) {
				this.itemProperty[i].animationDataPerson = animation.translateX(this.itemProperty[i].process*3).step().export()
			}
		},
		onHide() {
			for (var i = 0; i < this.itemProperty.length ;  i++) {
				this.itemProperty[i].animationDataProcess = ""
			}
			for (var i = 0; i < this.itemProperty.length ;  i++) {
				this.itemProperty[i].animationDataPerson = ""
			}
		},
		methods:{
			addNewSchedule: function(){
				uni.navigateTo({
					url: '/pages/newschedule/newschedule'
				})
			},
            setColor: function(e) {
				if(this.itemProperty[parseInt(e.currentTarget.dataset.id)]
						.tagItems[parseInt(e.currentTarget.dataset.tagid)]
						.nowTagColor == ""){
					this.itemProperty[parseInt(e.currentTarget.dataset.id)]
						.tagItems[parseInt(e.currentTarget.dataset.tagid)]
						.nowTagColor
						= this.itemProperty[parseInt(e.currentTarget.dataset.id)]
						.tagColor
					this.itemProperty[parseInt(e.currentTarget.dataset.id)]
						.tagItems[parseInt(e.currentTarget.dataset.tagid)]
						.fontColor
						= "rgb(255,255,255)"
				}
				else{
					this.itemProperty[parseInt(e.currentTarget.dataset.id)]
						.tagItems[parseInt(e.currentTarget.dataset.tagid)]
						.nowTagColor
						= ""
					this.itemProperty[parseInt(e.currentTarget.dataset.id)]
						.tagItems[parseInt(e.currentTarget.dataset.tagid)]
						.fontColor
						= "rgb(0,0,0)"
				}
            },
			changeDetailShow: function(e){
				var that = this
				if(this.itemProperty[parseInt(e.currentTarget.dataset.id)].itemDetail == false){
					this.itemProperty[parseInt(e.currentTarget.dataset.id)].itemDetail = true
					this.itemProperty[parseInt(e.currentTarget.dataset.id)].showAnimation = "down 0.2s"
				}
				else{
					this.itemProperty[parseInt(e.currentTarget.dataset.id)].showAnimation = "up 0.2s"
					that.itemProperty[parseInt(e.currentTarget.dataset.id)].itemDetail = false
				}
			},
		}
	}
</script>

<style>
	.detail-title-item{
		width: 100%;
		justify-content: center;
	}
	.detail-title-item-text{
		padding: 0upx 15upx;
		border-bottom: 1upx rgba(0,0,0,0.2) solid;
		color: rgba(0,0,0,0.2);
		font-size: 24upx;
	}
	@keyframes down{
		from{
			height: 0upx;
			bottom: 220upx;
		},
		to{
			height: 220upx;
			bottom: 0upx;
		}
	}
	@keyframes up{
		from{
			height: 220upx;
			bottom: 0upx;
		},
		to{
			height: 0upx;
			bottom: 220upx;
		}
	}
	.index {
		background-color: rgb(250,240,240);
		position: fixed;
		display: flex;
		flex-direction: column;
		top: var(--status-bar-height);
		width: 100%;
	}
	
	.nav-bar-userset{
		justify-content: space-between;
		display: flex;
		background-color: rgb(245,55,65);
		width: 750upx;
		height: 150upx;
	}
	.nav-bar-userset-logo{
		margin-top: 42upx;
		margin-left: 20upx;
		width: 110upx;
		height: 65upx;
	}
	.nav-bar-userset-add{
		margin-right: 45rpx;
		margin-top: 53upx;
		width: 40upx;
		height: 40upx;
	}
	
	.main-view{
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		display: flex;
		width: 750upx;
	}
	.time-process-block{
		z-index: 10;
		display: flex;
		flex-direction: column;
	}
	.date-view{
		display: flex;
		flex-direction: column;
		width: 750upx;
		background-color: rgb(171,216,200);
	}
	.week-view{
		display: flex;
		flex-direction: column;
		width: 750upx;
		height: 220upx;
		background-color: rgb(200,220,200);
	}
	.month-view{
		display: flex;
		flex-direction: column;
		width: 750upx;
		height: 220upx;
		background-color: rgb(235,235,190);
	}
	.year-view{
		display: flex;
		flex-direction: column;
		width: 750upx;
		height: 220upx;
		background-color: rgb(254,225,160);
	}
	.life-view{
		display: flex;
		flex-direction: column;
		width: 750upx;
		height: 220upx;
		background-color: rgb(247,211,126);
	}
	
	.top-line{
		z-index: 10;
		display: flex;
		align-items: center;
		height: 36upx;
		margin: 35upx 0upx 0upx 30upx;
	}
	.top-line .red-point{
		display: inline-block;
		width: 10upx;
		height: 10upx;
		border-radius: 5upx;
		background-color: rgb(245,0,0);
	}
	.top-line .time-name{
		display: inline-block;
		margin-left: 15upx;
		color: rgb(255,255,255);
		font-size:30upx;
		font-weight: 1000;
	}
	.top-line .precess-percent{
		color: rgb(255,255,255);
		display: inline-block;
		font-size:30upx;
		margin-left: 550upx;
		font-weight: 1000;
	}
	
	
	.all-process{
		z-index: 10;
		display: flex;
		flex-direction: column;
		margin: 0;
		border: 0;
		padding: 0;
		position: relative;
		bottom: 40upx;
		width: 100%;
	}
	.little-person{
		z-index: 10;
		position: relative;
		top: 20upx;
		display: flex;
		align-items: center;
		flex-direction: column;
		width: 100upx;
		margin: 0upx 0upx 0upx 45upx;
	}
	.little-person .little-person-image{
		display: inline-block;
		width: 20upx;
		height: 40upx;
	}
	.little-person .chat-frame{
		display: flex;
		align-items: center;
		flex-direction: column;
	}
	.little-person .chat-frame-image{
		display: inline-block;
		margin-bottom: 10upx;
		width: 100upx;
		height: 45upx;
	}
	.little-person .chat-frame-content{
		position: relative;
		top: 33upx;
		font-weight: 1000;
		font-size: 24upx;
	}
	
	.process-bar{
		z-index: 5;
		display: flex;
		align-items: center;
		margin: 0upx 0upx 0upx 30upx;
	}
	.process-bar .start-text{
		display: inline-block;
		text-align: center;
		margin: 0upx 0upx 0upx 0upx;
		width: 50upx;
		font-size:24upx;
		font-weight: 1000;
		color: rgb(255,255,255);
	}
	.process-bar .end-text{
		display: inline-block;
		text-align: center;
		margin: 0upx 0upx 0upx 0upx;
		width: 50upx;
		font-size:24upx;
		font-weight: 1000;
		color: rgb(255,255,255);
	}
	.process-bar .blank-bar{
		display: inline-block;
		margin: 0upx 20upx 0upx 20upx;
		height: 18upx;
		width: 570upx;
		background-color: rgb(255,255,255);
	}
	.process-bar .finish-bar{
		flex-wrap: nowrap;
		align-items: flex-start;
		position: relative;
		right: 642upx;
		margin: 0upx 0upx 0upx 0upx;
		height: 18upx;
		width: 1upx;
		background-color: rgb(255,0,0);
	}
	
	.schedule-detail-hidden{
		z-index: 1;
		position: relative;
		height: 0upx;
		bottom: 220upx;
		width: 100%;
	}
	.schedule-detail-show{
		z-index: 1;
		position: relative;
		height: 220upx;
		bottom: 0upx;
		width: 100%;
	}
	.schedule-detail-row{
		align-items: flex-start;
		flex-direction: row;
	}
	.all-tag-view{
		display: inline-block;
		width: 56%;
		height: 220upx;
		flex-wrap: wrap;
		justify-content: flex-start;
		margin: 0upx 0upx 5upx 40upx;
	}
	.tag-view{
		padding: 10upx 30upx;
		margin: 10upx 10upx;
		background-color: rgb(255,255,255);
		font-size: 24upx;
		height: 28upx;
		border-radius: 5upx;
	}
	.tag-view-up{
		flex-wrap: wrap;
	}
	.detail-note{
		height: 220upx;
		margin-top: 10upx;
		margin-bottom: 10upx;
		margin-right: 2%;
		width: 42%;
	}
	.detail-note-text{
		margin-top: 10upx;
		margin-bottom: 10upx;
		background-color: rgba(0,0,0,0.1);
		border-radius: 8upx;
		padding: 10upx;
		font-size: 24upx;
		color: #ffffff;
	}
	.detail-contain{
		align-items: flex-start;
		flex-direction: row;
		flex-wrap: nowrap;
	}
</style>
