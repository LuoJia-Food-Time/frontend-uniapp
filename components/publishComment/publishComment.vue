<template>
	<!-- 发评论 -->
	<view class="comment-publish-area">
		<view class="comment-publish-input-wrapper">
			<textarea @confirm="publishComment" @blur="textAreaBlur" v-model="newComment.content" class="comment-publish-input"
			 auto-height="true" required :placeholder="parentComment!==null ? '回复'+parentComment.userName+'：' : '写评论...' ">
			</textarea>
		</view>
		<view id="commentPublishButton" class="comment-publish-button" :class="newComment.content ? '' : 'comment-publish-button-gray'"
		 @click="publishComment">
			发送
		</view>
	</view>
</template>

<script>
	import httpUtils from '../../common/util/httpUtils.js';
	import comment from '../../components/comment/comment.vue';

	export default {

		components: {
			comment
		},

		data() {
			return {
				newComment: {
					momentId: null,
					content: "",
					parentId: 0,
					replyToId: 0
				},
			};
		},
		props: {

			parentComment: {
				type: Object
			},
			momentId: {
				type: Number
			},
			pageType: {
				type: String
			},
			parentId: {
				type: Number
			}
		},
		methods: {

			textAreaBlur(e) {
				console.log(e)
			},

			// 数据相关函数
			async publishComment() {
				if (!this.newComment.content) {
					uni.showToast({
						title: "评论不能为空",
						duration: 2000
					});
					return;
				}


				uni.showLoading({
					title: '发布中...'
				});
			

				
				this.newComment = {
					momentId: null,
					content: "",
					parentId: 0,
					replyToId: 0
				};

				uni.showToast({
					title: "发布成功",
					duration: 2000
				});
			}
		}
	}
</script>

<style>
	.comment-publish-area {
		background-color: white;
		width: 690rpx;
		padding: 0 30rpx;
		position: fixed;
		bottom: 0;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		height: 90rpx;
		border-top: 1px solid #f3f3f3;
		font-size: 28rpx;
	}

	.comment-publish-input-wrapper {
		background-color: white;
		height: 90rpx;
		max-height: 180rpx;
		width: 500rpx;
		overflow-y: auto;
	}

	.comment-publish-input {
		background-color: white;
		height: 90rpx;
		width: 500rpx;
		color: #333;
		font-size: 28rpx;
		padding-top: 26rpx;
	}

	.comment-publish-button-gray {
		color: #A1A1A1;
	}
</style>
