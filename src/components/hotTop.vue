<template>
	<div class="picturn">
		<div class="hotop">
			<div class="cloudmusic">
				<!-- <p class="p1">云音乐</p>
				<p class="p2">热歌榜</p> -->
			</div>
			<div class="update">
				<span>更新日期:</span>
				<span>12月29日</span>
			</div>
		</div>

	</div>
</template>

<script>
</script>

<style lang="less">
	.picturn {
		position: relative;
		padding-top: 38.9%;
		overflow: hidden;
		background: url(https://s3.music.126.net/mobile-new/img/hot_music_bg_2x.jpg?f01a252389c26bcf016816242eaa6aee=) no-repeat;
		background-size: contain;

		&::after {
			content: " ";
			position: absolute;
			left: 0;
			top: 0;
			right: 0;
			bottom: 0;
			z-index: 1;
			background-color: rgba(0, 0, 0, .2);
		}

		.hotop {
			width: 142px;
			height: 67px;
			position: absolute;
			top: 20px;
			left: 0;
			right: 0;
			bottom: 0;
			padding-left: 20px;
			z-index: 3;
			.cloudmusic {
				width: 142px;
				height: 67px;
				background: url(//s3.music.126.net/mobile-new/img/index_icon_2x.png?5207a28…=) no-repeat -24px -30px;
				background-size: 166px 97px;
			}

			.update {
				margin-top: 10px;
				color: hsla(0,0%,100%,.8);
				span{
					font-size: 14px;
				}
			}
		}

	}
</style>
