<template>
	<div class="play-full-footer">
		<div class="play-full-footer-icon">
			<!-- <span class="icon_collection">
				<svg>
					<path d="M16 28c0 0 2.11-1.591 2.259-1.704 2.168-1.707 3.155-2.51 4.483-3.692 2.147-1.911 3.825-3.7 4.974-5.417 0.822-1.229 1.357-2.402 1.565-3.528 0.941-5.091-1.221-8.588-5.151-9.44-2.959-0.641-6.218 0.432-8.131 2.659-1.975-2.525-5.247-3.477-8.295-2.5-3.688 1.182-5.83 4.758-5.040 9.323 0.245 1.418 1.093 2.956 2.449 4.636 1.061 1.314 2.415 2.69 4.029 4.142 1.441 1.296 2.502 2.165 4.774 3.968l2.085 1.554zM10.486 21.014c-1.541-1.384-2.825-2.687-3.811-3.906-1.164-1.44-1.863-2.706-2.040-3.729-0.624-3.599 0.95-6.222 3.685-7.098 2.629-0.842 5.444 0.239 6.747 2.866l0.66 1.331c0.123 0.248 0.327 0.246 0.452 0.003l0.678-1.323c1.177-2.295 4.186-3.559 6.84-2.985 2.842 0.615 4.363 3.073 3.61 7.141-0.154 0.83-0.581 1.766-1.265 2.788-1.038 1.55-2.611 3.224-4.642 5.030-1.289 1.145-2.254 1.929-4.377 3.599-0.119 0.090-0.852 0.651-1.024 0.769-0.025-0.020-0.783-0.597-0.931-0.68-2.173-1.723-3.202-2.567-4.582-3.806z"
						style="stroke: #000000;fill: #ffffff;fill-rule: nonzero;"></path>
				</svg>
			</span>
			<span class="icon_download">
				<svg>
					<path d="M14.7,1.6c0-0.9,0.7-1.6,1.6-1.6c0.9,0,1.6,0.7,1.6,1.6v19.2c0,0.9-0.7,1.6-1.6,1.6c-0.9,0-1.6-0.7-1.6-1.6V1.6
						z M16.3,20.7l9.6-9.8c0.6-0.6,1.6-0.4,2.2,0.3c0.6,0.6,0.6,1.6,0,2.3L17.9,24c-0.6,0.6-2.4,0.6-3,0L4,13.4c-0.6-0.6-0.6-1.6,0-2.3
						c0.6-0.6,1.6-0.6,2.3,0L16.3,20.7z M5.3,32c-0.9,0-1.6-0.7-1.6-1.6c0-0.9,0.7-1.6,1.6-1.6h21.3c0.9,0,1.6,0.7,1.6,1.6
						c0,0.9-0.7,1.6-1.6,1.6H5.3z"
						style="stroke: #000000;fill: #ffffff;fill-rule: nonzero;"></path>
				</svg>
			</span>
			<span class="icon_new">
				<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
					<circle cx="20" cy="20" r="15" stroke="#fff" stroke-width="2" fill="transparent" />
				</svg>
			</span>
			<span class="icon_information">
				<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
					<line x1="10" y1="11" x2="40" y2="11" style="stroke:rgb(255, 255, 255);stroke-width:2" />
					<line x1="10" y1="21" x2="40" y2="21" style="stroke:rgb(255, 255, 255);stroke-width:2" />
					<line x1="10" y1="31" x2="40" y2="31" style="stroke:rgb(255, 255, 255);stroke-width:2" />
				</svg>

			</span>
			<span class="icon_list">
				<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
					<circle cx="25" cy="15" r="1" stroke="#000000" stroke-width="2" />
					<circle cx="25" cy="25" r="1" stroke="#000000" stroke-width="2" />
					<circle cx="25" cy="35" r="1" stroke="#000000" stroke-width="2" />
				</svg>
			</span> -->
		</div>
		<div class="progresstime">
			<div class="progressleft"><span class="spanleft">{{currentTime | currentTimeprogress}}</span></div>
			<div class="progress">
				<input type="range" min="0" :max="duration" step="1" @input="getValue" :value="currentTime" />
				<span class="progressmiddle" :style="{ width: (currentTime / duration) * 100 + '%' }"></span>
			</div>
			<div class="progressright"><span class="spanright">{{duration | durationprogress}}</span></div>
		</div>
		<div class="Playplatoon">
			<div class="Play">
				<div class="Playright" @click="poplast">
					<svg height="50" width="50">
						<polygon points="18,26 38,11 38,38" style="fill:#FFF;stroke:rgb(255, 255, 255);stroke-width:1" />
						<line x1="18" y1="13" x2="18" y2="36" style="stroke:rgb(255, 255, 255);stroke-width:2" />
					</svg>
				</div>
				<div class="Playmiddle" @click="pop">
					<svg height="50" width="50" v-if="paused">
						<polygon points="38,26 18,13 18,36" style="fill:#FFF;stroke:rgb(255, 255, 255);stroke-width:1" />
					</svg>
					<svg height="50" width="50" v-else>
						<line x1="18" y1="13" x2="18" y2="36" style="stroke:rgb(255, 255, 255);stroke-width:2" />
						<line x1="30" y1="13" x2="30" y2="36" style="stroke:rgb(255, 255, 255);stroke-width:2" />
					</svg>
				</div>
				<div class="Playleft" @click="popnext">
					<svg height="50" width="50">
						<polygon points="38,26 18,13 18,36" style="fill:#FFF;stroke:rgb(255, 255, 255);stroke-width:1" />
						<line x1="38" y1="13" x2="38" y2="36" style="stroke:rgb(255, 255, 255);stroke-width:2" />
					</svg>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		props: ["currentTime", "duration","playlist","PlayNext","isShowPlayBar","isShowLyric","paused"],
		data: function() {
			return {};
		},
		filters: {
			durationprogress: function(value) {
				var minute;
				minute = Math.floor(value / 60);
				value = Math.floor(value % 60);
				// value  =   (value.length==1)?'0'+value:value;
				return minute + ":" + value
			},
			currentTimeprogress: function(value) {
				var minute;
				minute = Math.floor(value / 60);
				value = Math.floor(value % 60);
				// value  =   (value.length==1)?'0'+value:value;
				return minute + ":" + value
			}
		},
		methods: {
			getValue: function(e) {
				// console.log(e.target.value);
				this.$emit("update:currentTime", e.target.value);
			},
			pop:function(){
				this.$emit('togglePlayState')
				// this.isShowPlayBar=this.paused;
			},
			popnext:function(){
				this.$emit('PlayNext')
			},
			poplast:function(){
				this.$emit('PlayLast')
			},
		},
	};
</script>

<style lang="less">
	.play-full-footer {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;

		.play-full-footer-icon {
			width: 50px;
			height: 50px;
			// background-color: cornsilk;
			position: relative;
			display: flex;

			svg {
				path {
					color: #fff;
				}
			}

			.icon_collection {
				width: 50px;
				height: 40px;
				// background-color: skyblue;
				display: block;
				flex: 1 1 auto;
				// margin-left: 2.625rem;
				position: absolute;
				left: 4.375rem;
			}

			.icon_download {
				width: 50px;
				height: 40px;
				// background-color: oldlace;
				display: block;
				flex: 1 1 auto;
				position: absolute;
				left: 8.75rem;
			}

			.icon_new {
				width: 50px;
				height: 40px;
				// background-color: aqua;
				display: block;
				flex: 1 1 auto;
				position: absolute;
				left: 13.125rem;
			}

			.icon_information {
				width: 50px;
				height: 50px;
				// background-color: white;
				border-radius: 50%;
				display: block;
				flex: 1 1 auto;
				position: absolute;
				left: 17.5rem;

				svg {
					width: 50px;
					height: 50px;
					border-radius: 50%;
				}
			}

			.icon_list {
				width: 50px;
				height: 50px;
				border-radius: 50%;
				// background-color: palegreen;
				flex: 1 1 auto;
				margin-left: 21.875rem;

				svg {
					width: 50px;
					height: 50px;
				}
			}
		}

		.progresstime {
			display: flex;
			margin-top: 15px;

			.progressleft {
				width: 20%;
				height: 20px;
				// background-color: white;
				font-size: 10px;
				color: #c0c0c0;
				flex: 2 1 auto;

				span {
					padding-left: 40px;
				}
			}

			.progress {
				width: 60%;
				height: 1px;
				background: linear-gradient(to right, lightblue, lightcoral);
				position: relative;
				top: 6px;
				left: 0;
				margin: 0 auto;
				border-radius: 3px;
				flex: 1 1 auto;

				input {
					width: 100%;
					position: absolute;
					top: 0;
					left: 0;
					z-index: 99;
					opacity: 0;
				}

				.progressmiddle {
					display: block;
					position: absolute;
					top: 0;
					left: 0;
					width: 0%;
					height: 100%;
					// background: rgb(30, 124, 38);
					border-radius: 3px;
				}
			}

			.progressright {
				width: 20%;
				height: 20px;
				// background-color: white;
				font-size: 10px;
				color: #c0c0c0;
				flex: 1 1 auto;

				span {
					padding-left: 20px;
				}
			}
		}

		.Playplatoon {
			width: 100%;
			height: 100px;
			// background-color: skyblue;

			.Play {
				display: flex;
				margin-top: 5%;
				.Playleft {
					width: 50px;
					height: 50px;
					// background-color: palegreen;
					border-radius: 50%;
					margin-left: 10%;
					z-index: 5;
				}

				.Playmiddle {
					width: 50px;
					height: 50px;
					// background-color: oldlace;
					border: 1px solid #FFF;
					border-radius: 50%;
					margin-left: 10%;
					z-index: 5;
				}

				.Playright {
					width: 50px;
					height: 50px;
					// background-color: lavender;
					border-radius: 50%;
					margin-left: 20%;
					z-index: 5;
				}
			}

		}
	}
</style>
