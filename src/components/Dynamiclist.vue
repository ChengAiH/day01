<template>
	<div class="pylst_list">
		<!-- <div class="smtitle">
			<span class="Play_icon"></span>
			<span class="Play_whole">
				<p>播放全部</p>
			</span>
			<span class="Play_button">
				<button class="button"> + 收藏</button>
			</span>
		</div>
		<div class="smtitleList"></div> -->
	</div>
</template>

<script>
	export default {

	}
</script>

<style lang="less">
	.smtitle{
		width: 100%; 
		height: 55px;
		// background-color: paleturquoise;
		border-top-left-radius: 30px;
		border-top-right-radius: 30px;
		overflow: hidden;
		display: flex;
	}
	.Play_icon {
		display: inline-block;
		width: 22px;
		height: 22px;
		background-position: -24px 0;
		background-image: url(https://s3.music.126.net/mobile-new/img/index_icon_3x.png?49a82fee3e0fc602e9c8b25df2bda159=);
		background-size: 166px 97px;
		margin: 15px 0 0 15px;
		flex: 1 0 auto;
	}
	.Play_whole{
		margin: 15px 0 0 15px;
		flex: 4 0 auto;
		font-size: 20px;
		font-weight: 548;
	}
	.Play_button{
		width: 105px;
		height: 86%;
		background-color: pink;
		margin: 5px 30px 0 0;
		border-radius: 45px;
		overflow: hidden;
		border: none;
		flex: 1 0 auto;
		.button{
			width: 100%;
			height: 100%;
			background-color: #ff3a3a;
			border: none;
			color: #fff;
			font-size: 14px;
		}
	}
</style>
