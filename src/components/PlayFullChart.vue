<template>
	<div class="suspended" :class="{ paused: paused }" @click="suspend">
		<div class="middlepicturn">
			<img class="picturnimg" :src="picUrl" />
		</div>
	</div>
</template>

<script>
	export default {
		props: ["currentMusic", "isShowPlayBar", "paused"],
		methods: {
			suspend: function() {
				this.$emit('toggle-show-lyric')
				this.paused = false
			},
			// suspending:function(){
			// 	this.paused = false
			// }
		},
		computed:{
			picUrl:function(){
				let picarr;
				if(this.currentMusic.al){
					picarr=this.currentMusic.al.picUrl;
				}
				if(this.currentMusic.album){
					picarr=this.currentMusic.album.artist.img1v1Url;
				}
				if(this.currentMusic.picUrl){
					picarr=this.currentMusic.picUrl;
				}
				return picarr;
			}
		},
	}
</script>

<style scoped lang="less">
	.suspended {
		&.paused {
			.picturnimg {
				animation-play-state: paused;
			}
		}
	}

	.middlepicturn {
		width: 300px;
		height: 300px;
		margin: 0 auto;
		margin-top: 95px;

		.picturnimg {
			width: 100%;
			height: 100%;
			border-radius: 50%;
			animation: playpop 6s linear infinite;
			// box-shadow: 0 0 8px 0 rgba(0, 0, 0, 0.15);
		}

	}

	@keyframes playpop {
		form {
			transform: rotate(0deg);
		}

		to {
			transform: rotate(360deg);
		}
	}
</style>
