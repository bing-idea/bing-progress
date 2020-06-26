<template>
	<view class="content">
		<!-- 垂直进度条 -->
		<text class="info">垂直进度条</text>
		<view class="vertical">
			<!-- 事件监听 进度值绑定 -->
			<bing-progress class="bp" @change="change" @valuechange="change" @dragging="dragging" @gragstart="dragstart" @dragend="dragend" 
			direction="vertical" width="200px" :value="value" :step="10" 
			:subValue="subValue" backgroundColor="#ff0000"></bing-progress>
			<bing-progress class="bp" direction="vertical" width="200px" :value="value" :step="10"
			:subValue="subValue" backgroundColor="#ff0000" :reverse="true"></bing-progress>
			<!-- 垂直时在拖柄中显示进度值 须同时满足： direction="vertical" infoAlign="handle" :showinfo="true" -->
			<bing-progress class="bp" direction="vertical" infoAlign="handle" handleWidth="35px" handleHeight="45px" width="200px" :value="value" :step="10" 
			:subValue="subValue" :continuous="false"></bing-progress>
			<bing-progress class="bp" direction="vertical" width="200px" :max="-20" :min="120" 
			:value="value" :step="5" :subValue="subValue" :continuous="true" handleWidth="0"></bing-progress>
			<bing-progress class="bp" direction="vertical" width="200px" strokeWidth="3px" 
			handleHeight="10px" handleWidth="10px" :min="-20" :max="120" :value="value" :subValue="subValue"
			 :step="10" ></bing-progress>
		</view>
		<view class="center">
			<view class="btn-line">
				<button class="btn" @click="add">{{ addTimer?'停止':'增加'}}</button>
				<button class="btn" @click="reduce">{{ reduceTimer?'停止':'减少'}}</button>
				<button class="btn" @click="reset">归零</button>
			</view>
			<view class="showValue">
				<text>Value: {{value}}</text>
				<text>subValue: {{subValue}}</text>
			</view>
		</view>
		<!-- 水平进度条 -->
		<text class="info">水平进度条</text>
		<view class="horizontal">
			<!-- 反转  进度值在拖柄内 进度值字体大小设置 拖柄颜色设置-->
			<bing-progress class="bp" infoEndText="%" infoAlign="handle" infoColor="#ffffff" infoFontSize="14px" handleColor="#aa55ff" :reverse="true" barBorderRadius="20px" backgroundColor="#ff0000" bpBorderRadius="20px"
			:subValue="subValue" :value="value"></bing-progress>
			<!--圆角 主副进度步长设置 进度变化设置为非连续，即步进 进度值在中间-->
			<bing-progress class="bp" :value="20" infoAlign="center" :isActiveCircular="true" barBorderRadius="30px" infoContent="subValue" :step="10.5" :subStep="10" handleWidth="0" :continuous="false" :subContinuous="false"
			:subValue="subValue"></bing-progress>
			<!-- 进度值在左侧 设置进度值颜色-->
			<bing-progress class="bp" :max="100" infoAlign="left" :value="value" infoColor="#0000ff"
			:subValue="subValue" :step="10" :continuous="false" handleWidth="0"></bing-progress>
			<!-- 细进度条  最大值比最小值小-->
			<bing-progress class="bp" infoAlign="right" strokeWidth="3px" handleHeight="10px" handleWidth="10px" handleBorderRadius="5px"
			 :max="-20" :min="120" :value="value" :subValue="subValue"></bing-progress>
			<!-- 设置拖柄为图片 不显示进度值-->
			<bing-progress handleImgUrl="../../static/logo.png" :showInfo="false" handleBorderRadius="10px"></bing-progress>
			<!-- 设置为不可拖动 -->
			<bing-progress class="bp" infoAlign="handle" :value="value" :subValue="subValue" :disabled="true"></bing-progress>
		</view>
	</view>
</template>

<script>
	import bingProgress from '../../components/bing-progress/bing-progress.vue'
	export default {
		components: {
			bingProgress
		},
		data() {
			return {
				title: 'Hello',
				value: 0,
				subValue: 20,
				addTimer: null,
				reduceTimer: null,
				direction: 'vertical'
			}
		},
		onLoad() {
			
		},
		methods: {
			change(e) {
				console.log('change',e)
			},
			dragging(e) {
				console.log('ing',e)
			},
			dragend(e) {
				console.log('end',e)
			},
			dragstart(e) {
				console.log('start',e)
			},
			add() {
				if(this.reduceTimer) {
					clearInterval(this.reduceTimer)
					this.reduceTimer = null
				}
				if(this.addTimer) {
					clearInterval(this.addTimer)
					this.addTimer = null
				}
				else {
					this.addTimer = setInterval(()=>{
						this.value += 2
						this.subValue += 3
						if(this.value > 120) {
							clearInterval(this.addTimer)
							this.addTimer = null
						}
					},300)
				}
			},
			reset() {
				/*
				当通过 :value="pValue"当pValue=0时，如果拖动进度条改变进度值后，想要再通过设置pValue=0来使进度条的值再回到0是不可以的，
				因为vue的属性是单向绑定的，虽然拖动进度条后进度值变了，但是父组件中的pValue并没有改变，子组件也就无法监听到value值变化，
				所以就不会更新进度值，如果想要更新进度值，可以先给进度值设置一个非0值，短暂延迟后再设置为0，其他值也是一样的道理
				*/
				this.direction = this.direction=="vertical"?"horizontal":"vertical"
				this.value = 0.01
				this.subValue = 0.01
				/*
				错误写法，无效
				this.value = 0
				this.subValue = 0
				*/
			   // 正确写法
				setTimeout(()=>{
					this.value = 0
					this.subValue = 0
				}, 0)
			},
			reduce() {
				if(this.addTimer) {
					clearInterval(this.addTimer)
					this.addTimer = null
				}
				if(this.reduceTimer) {
					clearInterval(this.reduceTimer)
					this.reduceTimer = null
				}
				else {
					this.reduceTimer = setInterval(()=>{
						this.value -= 2
						this.subValue -= 5
						if(this.value < -20) {
							clearInterval(this.reduceTimer)
							this.reduceTimer = null
						}
					},300)
				}
			}
		}
	}
</script>

<style>
	.content {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.bp {
		margin: 5px;
	} 
	.horizontal {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: space-around;
		align-items: center;
	}
	.vertical {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
		width: 100vw;
	}
	.center {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.btn-line {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}
	.showValue {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
		width: 750rpx;
		padding: 5px;
	}
	.btn {
		font-size: 16px;
		margin: 5px;
	}
	.info {
		border-top-color: #ececec;
		border-top-width: 1px;
		border-top-style: solid;
		border-bottom-color: #ececec;
		border-bottom-width: 1px;
		border-bottom-style: solid;
		width: 100vw;
		text-align: center;
		background-color: #f8f8f8;
		padding: 5px;
		font-size: 16px;
	}
</style>
