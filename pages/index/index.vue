<template>
	<view>
		<view class="" style="background-image: url(../../static/bg.jpg);position: fixed;width: 100vw;height: 100vh;">
		</view>
		<view style="">
			<view class=" flex align-center flex-wrap"
				style="position: fixed;width: 100vw;height: 90upx;z-index: 10;background-color: #9E638F;opacity: 0.8;">
				<view class="padding-left text-xxl text-bold text-white" @click="ToIndex()">
					{{this.title}}
				</view>
				<view class="padding-left text-center text-white self-center">
					version:{{result.info.version}}
				</view>
			</view>
			<view class="" style="padding-top: 70upx;">
				<view class="flex justify-center align-center relative">
					<view class="flex flex-wrap justify-center api-port">
						<view class="flex flex-wrap align-center full-width">
							<view class="padding-left text-content text-lg auto-width full-height">
								<text>当前API接口：</text>
							</view>
							<view class="select ">
								<view class="flex align-center select-text full-width"
									@click="show_select=!show_select"><text
										class="padding-left text-cut">{{api_tag}}</text>
									<view class="cuIcon-unfold" style="margin-left:auto;padding-right: 15px;"></view>
								</view>

								<view class=" select-content text-cut"
									:class="show_select?'select-animation':'animation-slide-top hidden'">
									<view class="option" v-for="value in tag" v-model="tag" @click="change_api_tag">
										<view class="padding-left full-height full-width flex align-center"
											:data-api-tag="value">{{value}}</view>
									</view>
								</view>
							</view>
							<view class="text-Abc" style="margin-left:auto;padding-right: 15px;">
								当前openapi版本：{{result.openapi}}
							</view>
						</view>

					</view>
				</view>
				<view class="flex justify-center align-center" style="padding-bottom: 100rpx;">
					<view class="flex flex-wrap justify-center "
						style="width: 90vw;align-items: flex-start;background-color: rgba(255,255,255,0.7);z-index: 1;">

						<view class="cu-card case cu-card animation-slide-bottom"
							v-for="(item,result_key,result_index) in result.paths"
							style="width: 16vw;min-width: 350px;box-sizing: border-box;opacity: 1.0;">
							<view class="cu-item shadow" v-if="item_value.tags.includes(api_tag)" @tap="showModal"
								:data-modal-data="item" :data-modal-url="result_key" data-target="Modal"
								v-for="(item_value,item_key,item_index) in item">
								<view class="image">
									<image src="../../static/backgroundjpg.jpg" widthFix style="height: 400rpx;">
									</image>
									<view class="cu-tag text-ABC" :class="item_key == 'get' ? 'bg-cyan':'bg-blue'">
										{{item_key}}
									</view>
									<view class="cu-bar bg-shadeBottom"> <text class="">{{item_value.summary}}</text>
									</view>
								</view>
								<view class="cu-list padding">
									<view class="cu-item">
										<view class=" flex-sub text-left">
											<view class="text-grey text-cut">{{result_key}}</view>
										</view>
									</view>
								</view>
							</view>
						</view>
						<view class="cu-card case cu-card "
							style="width: 16vw;min-width: 350px;box-sizing: border-box;">
						</view>
						<view class="cu-card case cu-card "
							style="width: 16vw;min-width: 350px;box-sizing: border-box;">
						</view>
						<view class="cu-card case cu-card "
							style="width: 16vw;min-width: 350px;box-sizing: border-box;">
						</view>
						<view class="cu-card case cu-card "
							style="width: 16vw;min-width: 350px;box-sizing: border-box;">
						</view>
						<view class="cu-card case cu-card "
							style="width: 16vw;min-width: 350px;box-sizing: border-box;">
						</view>
						<view class="cu-card case cu-card "
							style="width: 16vw;min-width: 350px;box-sizing: border-box;">
						</view>
					</view>
				</view>

				<view class="flex justify-center footer" style="">
					<view class="">
						<view class="flex flex-wrap text-white">

							<view class="text-left self-center" style="width: 1000rpx;">
								<text class="text-xxl text-bold">关于 {{title}}<br></text>
								<text class="text-xl">{{result.info.description}}<br></text>
								<br><br>
								<text class="text-xxl">
									反馈及建议<text class="cuIcon-down"></text><br>
									<a :href="'mailto:'+self_conf.MAIL"
										style="text-decoration: none;color: #FFFFFF;"><text style="font-size: 55upx;"
											class="cuIcon-mail"></text></a></text>

								<a :href="'http://wpa.qq.com/msgrd?v=3&uin='+self_conf.QQ+'&site=qq&menu=yes'"
									style="padding-left: 15px;">
									<image src="../../static/QQlogo.png" mode="aspectFill"
										style="width: 55upx;height: 55upx;"></image>
								</a>
							</view>
							<view class="text-left self-center" style="padding-left: 40rpx;width: 500rpx;">
								<text class="text-xxl text-bold">投石区<text class="cuIcon-down"></text><br></text>
								<view class="flex   text-center" style="width: 800rpx;">
									<view class="" style="flex: 1;">
										<image src="../../static/wechat.png" mode=" aspectFill"
											style="width: 250rpx;height: 250rpx;"></image>
										<text>微信</text>
									</view>
									<view class="" style="flex: 1;">
										<image src="../../static/alipay.png" mode=" aspectFill"
											style="width: 250rpx;height: 250rpx;"></image>
										<text>支付宝</text>
									</view>
									<view class="" style="flex: 1;">
										<image src="../../static/qq.jpg" mode=" aspectFill"
											style="width: 250rpx;height: 250rpx;"></image>
										<text>QQ</text>
									</view>
								</view>
							</view>
						</view>
						<view class="flex align-center justify-center" style="padding-top: 50px;">
							© 2021 {{title}} <a href="https://beian.miit.gov.cn/" class="text-black"
								style="text-decoration: none;padding-left: 30px;">网络备案号:{{self_conf.FILING}}</a>
						</view>
					</view>

				</view>
				<view class="cu-modal" :class="modalName=='Modal'?'show animation-slide-bottom':''"
					v-for="(modal_value,modal_key,modal_index) in modalData">
					<view class="cu-dialog "
						style="width: auto;min-width: 100vw;background-color: #F1F1F1;min-height: 100vh;">
						<view class="cu-bar bg-white solid-bottom "
							style="text-align: right;justify-content: flex-end;background-color: #F1F1F1;">
							<view class="action" @tap="hideModal">
								<text class="cuIcon-close text-red"></text>
							</view>
						</view>

						<view class=" flex solid-bottom solid ">
							<view class=" "
								style="flex: 2;max-height: 92vh;min-height: 92vh;overflow: auto;min-width: 100px;padding: 30px;">
								<view class=" text-left" style="background-color: #F1F1F1;height: 100%;">
									<text class="text-sl" v-for="value in modal_value.tags">{{modalUrl}}
										<view class='cu-tag round bg-orange lg text-ABC' style="margin-left: 15px;">
											{{modal_key}}
										</view>
										<view class='cu-tag round bg-cyan lg' style="margin-left: 15px;">{{value}}
										</view><br>
									</text>
									<view class="padding-bottom">
									</view>
									<text class="text-xxl">概要：{{modal_value.summary}}<br></text>
									<text>备注：{{modal_value.description}}<br></text>
									<view class="padding-bottom">
									</view>
									<text class="text-xl "
										v-if="modal_value.hasOwnProperty('requestBody')">参数:</text><br>
									<view class="solid" v-if="modal_value.hasOwnProperty('requestBody')">

										<view class="" v-for="(item,key,index) in modal_value.requestBody.content">
											<text class="text-xl">Accept header:{{key}}<br>
												<text class="text-Abc">type:{{item['schema']['type']}}</text>
											</text>
											<view class="padding-bottom">
											</view>
											<view class="">
												<uni-table stripe emptyText="暂无更多数据" :border="true"
													style="max-width: 100%;">
													<uni-tr>
														<uni-th align="center" class="text-Abc">key</uni-th>
														<uni-th align="center" class="text-Abc">type</uni-th>
														<uni-th align="center" class="text-Abc">必须</uni-th>
														<uni-th align="center" class="text-Abc">格式(format)</uni-th>
														<uni-th align="center" class="text-Abc">默认值</uni-th>
														<uni-th align="center" class="text-Abc">备注</uni-th>
													</uni-tr>
													<uni-tr
														v-for="(properties_item,properties_key,index) in item['schema']['properties']">
														<uni-td align="center">{{properties_key}}</uni-td>
														<uni-td align="center">
															<view v-for="(info,key) in properties_item"
																v-if="key == 'type'">{{info}}</view>
															<view v-else></view>
														</uni-td>
														<uni-td align="center">
															<view v-if="modal_value.requestBody['required'] == true">
																<text class="cuIcon-check"></text>
															</view>
															<view
																v-else-if="item['schema']['required'].includes(properties_key)">
																<text class="cuIcon-check"></text>
															</view>

															<view v-else></view>
														</uni-td>
														<uni-td align="center">
															<view v-for="(info,key) in properties_item"
																v-if="key == 'format'">{{info}}</view>
															<view v-else></view>
														</uni-td>
														<uni-td align="center">
															<view v-for="(info,key) in properties_item"
																v-if="key == 'default'">{{info}}</view>
															<view v-else></view>
														</uni-td>
														<uni-td align="center">
															<view v-for="(info,key) in item.example"
																v-if="key == properties_key ">{{info}}</view>
															<view v-else></view>
														</uni-td>
													</uni-tr>
												</uni-table>
											</view>
										</view>

									</view>

									<view class="padding">

									</view>
									<view class="" v-for=" (item,key,index) in modal_value.responses">

										<text class="text-lg text-gray   "><text
												class="cuIcon-titles text-orange "></text>状态码 {{key}}
										</text>
										<view class="code flex align-start "
											style="text-align: left;margin-top: 15px;margin-bottom: 15px;">
											{{modal_value.responses[key]}}

										</view>

									</view>
								</view>
							</view>
							<!-- <view class=""
								style="flex: 2;max-height: 92vh;overflow: auto;min-height: 92vh;min-width: 20vw;padding: 15px;">
								<view class=" "
									style="text-align: left;padding: 15px;background-color: #F1F1F1;background-color: #F1F1F1;">
									<view class="" v-for=" (item,key,index) in modal_value.responses">

									<text class="text-lg text-gray padding "><text
											class="cuIcon-titles text-orange "></text>{{key}}
											</text>
									<view class="code flex align-start " style="text-align: left;margin: 15px;">
										{{modal_value.responses[key]}}
									</view>
								</view>
							</view>

						</view> -->
							<view class="solid"
								style="flex: 3;max-height: 92vh;overflow: hidden;min-width: 20vw;padding: 30px;">
								<view class="text-left solid" style="padding: 1vh;">
									<text class="text-Abc">response</text>
								</view>
								<view class="response-code" style="min-height: 20vh;height: auto;">
									{{modal_value}}

								</view>
								<view class="text-left  " style="padding: 1vh;">
									<text class="text-Abc">请求测试</text>
								</view>
								<view class="response-form flex text-left padding solid full-width"
									style="min-height: 55vh; user-select: none;">
									<form @submit="formSubmit" class="full-width">

										<view class="solid" v-model="modal_value.requestBody"
											v-if="modal_value.hasOwnProperty('requestBody')">
											<input type="text" :value="modalUrl">
											<view class="" v-for="(item,key,index) in modal_value.requestBody.content">

												<view class="title  text-left"
													style="font-size: 40upx;padding-left: 15px;display: flex;flex-wrap: wrap;">
													<view class="flex  align-center text-left full-width">

														<view class="flex text-left align-center"
															style="min-width: 15%;max-width:15%;height:100upx;">
															<view>Accept header:</view>
														</view>

														<view class=""
															style="padding-left: 30px;min-width: 85%;max-width:85%;"
															v-if="key">
															<input class="resp-input" style="" :value="key" name="input"
																placeholder="" disabled="disabled" />
														</view>
														<view class="" v-else></view>
													</view>
												</view>

												<view class="title  text-left"
													style="font-size: 40upx;padding-left: 15px;display: flex;flex-wrap: wrap;">
													<view class="full-width" v-for="(items,key,index) in item">
														<view class="flex  align-center text-left full-width flex-wrap" style=""
															v-for="(info,key,index) in items['properties']">
															<view class="flex text-left align-center"
																style="min-width: 15%;max-width:15%;height:100upx;">
																<view>{{key}}:</view>
															</view>
															<view class=""
																style="padding-left: 30px;min-width: 85%;max-width:85%;"
																v-if="key">
																<view class="" @click="upload_image()" v-if="key == 'file'">
																	点击上传
																</view>
																<view class="" v-else>
																	<input type="file" v-if="info['format']">
																	<input class="resp-input" style=""
																		:value="info['default'] || null" :name="key"
																		:placeholder="'类型为'+info['type']" />
																</view>
															</view>
															<view class="" v-else></view>
															
														</view>
													</view>
												</view>
												<view class="uni-btn-v">
													<button form-type="submit">提交</button>
												</view>
											</view>
										</view>
									</form>
									<view class="padding">

									</view>
								</view>
								<!-- <view class=" "
									style="margin-top: 15px;text-align: left;padding: 15px;background-color: #F1F1F1;"
									v-for="(item,key,index) in modal_value.requestBody">
									<text class="text-lg text-gray padding-left"><text
											class="cuIcon-titles text-orange"></text>{{key}}</text>
									<view class="code flex align-start" style="text-align: left;margin-top: 15px;">
										{{modal_value.requestBody[key]}}
									</view>
								</view> -->
							</view>
						</view>
					</view>
				</view>

			</view>
		</view>
	</view>
</template>

<script>
	import $RefParser from "@apidevtools/json-schema-ref-parser";
	import ajax from '../../common/ajax.js'
	import $ from '@/jquery/jquery-3.4.1.min.js'
	export default {
		data() {
			return {
				ColorList: this.ColorList,
				modalName: null,
				tval: "value1",
				title: '',
				show_select: false,
				result: uni.getStorageSync('result'),
				tag: [],
				api_tag: '',
				self_conf: require('@/common/conf.json'),
				modalData: [],
				modalUrl: ''
			}
		},
		onLoad() {},
		onShow() {

			// this.ToggleDelay()
		},
		onReady() {
			this.get_openapi_json()
			this.sort_tags()
		},
		methods: {
			upload_image() {
				uni.chooseImage({
					count: 1,
					sizeType: ['original'],
					sourceType: ['album'],
					success: function(res) {
						const temp = res.tempFilePaths;
						console.log(temp)
						uni.setStorageSync('image', temp)
					}
				})
			},
			formSubmit: function(e) {
				console.log(JSON.stringify(e.detail.value))
				var formdata = e.detail.value
				uni.showModal({
					content: '表单数据内容：' + JSON.stringify(formdata),
					showCancel: false
				});
				this.request_to_api_interface()
			},
			request_to_api_interface() {
				var baseUrl = this.self_conf.DOMAIN
				var url = this.modalUrl
				console.log(baseUrl, url)
				$.ajax({
					type: "GET",
					url: "test.json",
					data: {
						username: $("#username").val(),
						content: $("#content").val()
					},
					dataType: "json",
					success: function(data) {
						$('#resText').empty(); //清空resText里面的所有内容
						var html = '';
						$.each(data, function(commentIndex, comment) {
							html += '<div class="comment"><h6>' + comment['username'] +
								':</h6><p class="para"' + comment['content'] +
								'</p></div>';
						});
						$('#resText').html(html);
					},
					failed: function(err) {
						alert(err)
					}
				});
			},
			showModal(e) {
				document.body.style.height = '100vh';
				document.body.style['overflow'] = 'hidden';
				this.modalName = e.currentTarget.dataset.target
				this.modalData = ''
				this.modalData = e.currentTarget.dataset.modalData
				this.modalUrl = e.currentTarget.dataset.modalUrl
			},
			hideModal(e) {
				this.modalData = []
				this.modalName = null
				document.body.style.height = 'unset';
				document.body.style['overflow'] = 'auto';
			},
			change_api_tag(e) {
				this.api_tag = e.target.dataset.apiTag
				this.show_select = false
				console.log(e.target.dataset.apiTag)
			},
			selectitem(index, item) {
				console.log(item)
				if (index >= 0) {
					this.tval = item.value;
				} else {
					this.tval = ""
				}
			},
			get_json_schema_refs_value() {
				let parser = new $RefParser();

				parser.dereference(this.result);
				console.log(parser.$refs.get(
					"#/components/schemas/Body_compressed_to_specified_size_api_compressed_to_specified_size_post"
				))

			},
			ToIndex() {
				location.href = '/'
			},
			sort_tags() {
				var paths = this.result.paths
				for (var i in paths) {
					if (paths[i].hasOwnProperty('get')) {
						for (var j = 0; j < paths[i]['get']['tags'].length; j++) {
							if (!this.tag.includes(paths[i]['get']['tags'][j])) {
								this.tag.push(paths[i]['get']['tags'][j])
							}
						}
					} else {
						for (var j = 0; j < paths[i]['post']['tags'].length; j++) {
							if (!this.tag.includes(paths[i]['post']['tags'][j])) {
								this.tag.push(paths[i]['post']['tags'][j])
							}
						}
					}
				}
				this.api_tag = this.tag[0]

			},
			ToggleDelay() {
				this.toggleDelay = true;
				setTimeout(() => {
					this.toggleDelay = false
				}, 1000)
			},
			get_openapi_json() {
				ajax.get({
					header: {
						'accept': 'application/json'
					},
					url: '/openapi.json',
					param: {}
				}).then((res) => {
					if (res.data.code == 404) {
						uni.showToast({
							title: res.data.msg,
							duration: 2000
						});
					} else {
						this.title = res.data.info.title
						uni.setNavigationBarTitle({
							title: res.data.info.title
						})
						uni.setStorageSync('result', res.data)
						console.log(Object.keys(this.result.paths).length)
						console.log(this.result)
						this.get_json_schema_refs_value()
					}
				})
			}
		}
	}
</script>

<style>
	@import "../../colorui/animation.css";

	.select-content::-webkit-scrollbar {
		display: none;
	}

	/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
	/* .select-content::-webkit-scrollbar {
		width: 16upx !important;
		height: 16upx !important;
		background-color: #F5F5F5;
	} */

	/*定义滚动条轨道 内阴影+圆角*/
	/* .select-content::-webkit-scrollbar-track {
		// -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
		border-radius: 10px;
		background-color: #fff;
	} */

	/*定义滑块 内阴影+圆角*/
	/* .select-content::-webkit-scrollbar-thumb {
		border-radius: 10px;
		-webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, .3);
		background-color: #555;
	} */


	.footer {
		background-position: center top;
		background-size: cover;
		background-color: #9E638F;
		padding-top: 80rpx;
		height: 30vh;
		position: relative;
	}

	.footer::after {
		background-color: #9E638F;
		padding-top: 80rpx;
		height: 30vh;
		position: relative;
		background-position: center top;
		background-size: cover;
		background-attachment: fixed;
		-webkit-filter: blur(20px);
		-moz-filter: blur(20px);
		-ms-filter: blur(20px);
		-o-filter: blur(20px);
		filter: blur(20px);
	}

	.resp-input {
		background-color: #F0F0F0;
		font-size: 40upx;
		height: 100upx;
		border-bottom: 1px solid #000;
		border-top: 0px;
		border-left: 0px;
		border-right: 0px;
		justify-content: flex-end;
	}

	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.select {
		z-index: 20;
		text-align: left;
		width: 400rpx;
		height: 3vh;
		/* border: 1rpx solid #99955C; */
	}

	.select-text {
		width: 400rpx;
		height: 3vh;
		border-radius: 1px;
		/* border: 1rpx solid #99955C; */
		background-color: #99765C;
		opacity: 0.8;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.relative {
		position: relative;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}

	.hidden {
		display: none;
	}

	.api-port {
		color: #FFFFFF;
		padding: 100rpx;
		width: 90vw;
		align-items: flex-start;
	}

	.select-animation {
		animation-name: select;
	}

	.full-width {
		width: 100%;
	}

	.full-height {
		height: 100%;
	}

	.auto-width {
		width: auto;
	}

	.auto-height {
		height: auto;
	}

	.option {
		height: 3vh;
		width: 400rpx;
		border-radius: 1px;
		border: 1rpx solid #99955C;
		background-color: #99765C;
	}

	.code {
		white-space: pre-wrap;
		word-break: break-all;
		word-wrap: break-word;
		text-align: left;
		background-color: #2C405A;
		color: #F1F1F1;
		padding-left: 36px;
		opacity: 0.5;
		padding-bottom: 15px;
	}

	.response-code {
		white-space: pre-wrap;
		word-break: break-all;
		word-wrap: break-word;
		text-align: left;
		background-color: #2C405A;
		color: #F1F1F1;
		padding-left: 36px;
		opacity: 0.5;
		min-height: 20vh;
		max-height: 30vh;
		padding-bottom: 15px;
		overflow: auto;
	}

	.select-content {
		border-radius: 1px;
		max-height: 25vh;
		position: relative;
		height: auto;
		overflow-y: scroll;
		overflow-x: hidden;
		z-index: 1;
	}

	/* Animation css */
	[class*=-animation] {
		animation-duration: .8s;
		animation-timing-function: ease-out;
		animation-fill-mode: both
	}

	@keyframes select {
		0% {
			opacity: 0;
			transform: translateY(-1%)
		}

		100% {
			opacity: 1;
			transform: translateY(0)
		}
	}
</style>
