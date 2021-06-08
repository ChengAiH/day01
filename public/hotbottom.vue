<template>
	<ul>
		<li class="lis" v-for="(songing,index) in HotbottomSong" :key="index" @click="Playhot({item:songing,index})">
			<div class="infotop">
				<p>
					<span>0{{index+1}}</span>
					<span>{{songing.al.name}}</span>
				</p>

				<p v-for="(songok,index) in songing.ar" :key="index">
					<i class="sghoting"></i>
					<span class="three">{{songok.name}}</span>
					<span class="three">{{songok.ar.name}}</span>
				</p>
			</div>
			<div class="icon">
				<span  
					class="playing" 
					:class="{ paused: paused }"
					v-if="currentMusic && currentMusic.id"
				>
					<i></i>
					<i></i>
					<i></i>
				</span>
				<span class="Playicon" v-else>▶</span>
			</div>
		</li>
		<!-- <Hotbottomsong
			v-for="(songing,index) in HotbottomSong"
			:key="index"
		></Hotbottomsong> -->
	</ul>
</template>

<script>
	// import Hotbottomsong from "@/components/Hotbottomsong.vue";
	export default {
		props: ["HotbottomSong","currentMusic","paused"],
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
		}
		// components:{
		// 	Hotbottomsong,
		// }
	}
</script>

<style lang="less">
	.lis {
		margin: 8px 0 0 10px;
		line-height: 23px;

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

		.icon {
			width: 30px;
			height: 30px;
			float: right;
			.Playicon {
				display: inline-block;
				width: 25px;
				height: 25px;
				padding-left: 7px;
				line-height: 22px;
				border-radius: 50%;
				border: 1px solid #ccc;
				color: #ccc;
				font-size: 14px;
			}

			.playing {
				display: flex;
				justify-content: space-between;
				align-items: flex-end;

				i {
					width: 6px;
					height: 30px;
					background: red;
					// display: inline-block;
					transform-origin: center bottom;

					animation: playes 0.6s linear -0.2s infinite alternate-reverse;

					&:first-of-type {
						animation-delay: 0s;
					}

					&:last-of-type {
						animation-delay: -0.4s;
					}
				}

				&.paused {
					i {
						animation-play-state: paused;
					}
				}
			}
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
