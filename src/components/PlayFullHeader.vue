<template>
	<div class="boxtop">
		<div class="returnhome" @click="$emit('show-play-bar')">
			<svg class="svgs" xmlns="http://www.w3.org/2000/svg" version="1.1" width="50" height="50">
				<line x1="0" y1="15" x2="15" y2="0" style="stroke:rgb(255, 255, 255);stroke-width:2" />
				<line x1="0" y1="15" x2="30" y2="15" style="stroke:rgb(255, 255, 255);stroke-width:2" />
				<line x1="0" y1="15" x2="15" y2="30" style="stroke:rgb(255, 255, 255);stroke-width:2" />
			</svg>
		</div>
		<div class="middleinformation">
			<!-- <p class="middleone">{{currentMusic.name}}</p> -->
			<p class="middlewritle"
				v-for="(ISongs,index) in picname||currentMusic.song.artists"
				:key="index"
			><template v-if="index"> / </template>{{ ISongs.name }}</p>
		</div>
		<div class="share">
			<div 
				class="headportrait"
			>
				<img src="http://p4.music.126.net/6y-UleORITEDbvrOLV0Q8A==/5639395138885805.jpg"/>
			</div>
			<!-- <div class="sharelink">
				<i class="list_icon_share"></i>
			</div> -->
		</div>
	</div>
<!-- currentMusic.ar||currentMusic.song.artists -->
</template>

<script>
	export default {
		props:["currentMusic"],
		computed:{
			picname:function(){
				let picnama;
				if(this.currentMusic.artists){
					picnama=this.currentMusic.artists;
				}
				if(this.currentMusic.ar){
					picnama=this.currentMusic.ar;
				}
				console.log(picnama)
				return picnama;
			}
		},
	}
</script>

<style lang="less">
	.boxtop {
		width: 100%;
		height: 50px;
		// background-color: white;
		color: white;
		display: flex;
		.returnhome {
			width: 30px;
			height: 30px;
			color: black;
			padding: 5px 0 0 0;
			flex: 5 1 auto;
			.svgs{
				margin-top: 9px;
				margin-left: 22px;
				color: white;
			}
		}

		.middleinformation {
			width: 150px;
			height: 100%;
			padding: 10px 0 0 15px;
			flex: 4 1 auto;
			.middlewritle{
				padding-top: 5px;
				font-size: 13px;
				color: #C0C0C0;
				float: left;
			}
		}

		.share {
			width: 150px;
			height: 100%;
			padding: 10px 0 0 35px;
			padding-left: 15px;
			flex: 0.2 1 auto;
			.headportrait{
				width: 50px;
				height: 50px;
				background-size: cover;
				border-radius: 50%;
				display: inline-block;
				img{
					width: 100%;
					height: 100%;
					border-radius: 50%;
				}
			}
		}
	}
</style>
