<template>
	<ul>
		<li class="lis" v-for="(songing,index) in HotbottomSong" :key="index" @click="Playhot({item:songing,index})">
			<div class="infotop">
				<p>
					<span>{{index+1}}</span>
					<span>{{songing.al.name}}</span>
				</p>

				<p>
					<i class="sghoting"></i>
					<span class="three">{{songing.name}}</span>-
					<span class="three" v-for="(songok,index) in songing.ar" :key="index">
						<template v-if="index"> / </template>{{ songok.name }}
					</span>
				</p>
			</div>
		<Hotbottomsong
			class="Hotbottomsong"
			:songing="songing"
			:HotbottomSong="HotbottomSong"
			:paused="$attrs.paused"
			:currentMusic="$attrs.currentMusic"
		></Hotbottomsong>
		</li>
		<!-- <Hotbottomsong
			v-for="(songing,index) in HotbottomSong"
			:key="index"
		></Hotbottomsong> -->
		<!-- v-for="(songok,index) in songing.ar" :key="index" -->
	</ul>
</template>

<script>
	import Hotbottomsong from "@/components/Hotbottomsong.vue";
	export default {
		props: ["HotbottomSong"],
		data: function() {
			return {
				HotbottomSongs: [],
			}
		},
		methods: {
			Playhot: function(songing) {
				console.log(songing)
				this.$emit('update:music', songing)
			}
		},
		components:{
			Hotbottomsong,
		}
	}
</script>

<style lang="less">
	.lis {
		margin: 8px 0 0 10px;
		line-height: 23px;
		padding: 8px 0 0 6px;
		
		.sghoting {
			display: inline-block;
			width: 12px;
			height: 8px;
			margin-right: 4px;
			margin-bottom: 2px;
			background: url(https://s3.music.126.net/mobile-new/img/index_icon_2x.png?5207a28c3767992ca4bb6d4887c74880=) no-repeat;
			background-size: 166px 97px;
			font-size: 12px;
			color: #888;
		}
		.three{
			font-size: 12px;
			color: #888;
		}
		.Hotbottomsong{
			float: right;
			margin-top: -35px;
			margin-right: 10px;
		}

	}

	@keyframes playes {
		from {
			// height: 50px;
			transform: scaleY(1);
		}

		to {
			// height: 10px;
			transform: scaleY(0.2);
		}
	}
</style>
