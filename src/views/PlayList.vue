<template>
	<div class="playlists">
		<!-- <div class="return"  @click="returnm"></div> -->
		<section class="plhead">
			<div class="box" :style="{backgroundImage: 'url('+this.$route.query.item.picUrl+')'}"></div>
			<div class="plhead_wrap">
				<div class="plhead_picture">
					<img class="u_img" :src="this.$route.query.item.picUrl" />
					<span class="Isthd">歌单</span>
					<i class="Isthd_num">{{this.$route.query.item.playCount | classonclick}}</i>
				</div>
				<div class="plhead_writter">
					<h2 class="thind">{{this.$route.query.item.name}}</h2>
					<div class="avater">
						<p class="p_avater">{{this.$route.query.item.copywriter}}</p>
					</div>
				</div>
			</div>
			<!-- <div class="middlebottom"></div> -->
		</section>
		<Dynamiclist></Dynamiclist>
		<marvellous
		:aggregateone="aggregateone"
		></marvellous>
		<newest
		:aggregatetwo="aggregatetwo"
		></newest>
	</div>
</template>

<script>
	import Dynamiclist from "@/components/Dynamiclist.vue"
	import marvellous from "@/components/marvellous.vue"
	import newest from "@/components/newest.vue"
	export default {
		components: {
			Dynamiclist,
			marvellous,
			newest,
		},
		data:function(){
			return{
				aggregateone:[],
				aggregatetwo:[],
			}
		},
		created() {
			this.axios
				.get("/comment/playlist?id=" + this.$route.query.item.id)
				.then((response) => {
				// console.log(response.data.hotComments)
				// console.log(response.data.comments)
				this.aggregateone = response.data.hotComments;
				this.aggregatetwo = response.data.comments;
				})
		},
		filters: {
			classonclick: function(value) {
				return (value / 10000).toFixed(1) + "涓";
			},
		},
		methods:{
			returnm:function(){
				this.$emit('show-play-bar');
			}
		},
		
	}
</script>

<style lang="less">
	.playlists {
		background-color: #fff;
		min-height: 100%;
		.return{
			width: 30px;
			height: 30px;
			background-color: skyblue;
		}
		// padding-left: env(safe-area-inset-left);
		// padding-right: env(safe-area-inset-right);
		// padding-bottom: env(safe-area-inset-bottom);
		.plhead {
			position: relative;
			padding: 30px 10px 30px 15px;
			overflow: hidden;
			font: 14px/1.5 Helvetica, sans-serif, STHeiTi;

			.box {
				position: absolute;
				left: 0;
				top: 0;
				right: 0;
				bottom: 0;
				z-index: 1;
				width: 100%;
				height: 500px;
				background-size: cover;
				background-repeat: no-repeat;
				background-position: 50%;
				filter: blur(20px);
				-webkit-transform: scale(1.5);
			}

			.plhead_wrap {
				position: relative;
				display: flex;
				z-index: 2;
				font: 14px/1.5 Helvetica, sans-serif, STHeiTi;

				.plhead_picture {
					width: 35vw;
					position: relative;
					background-color: #e2e2e3;

					.u_img {
						width: 100%;
						vertical-align: middle;
					}

					.Isthd {
						position: absolute;
						z-index: 3;
						top: 10px;
						left: 0;
						padding: 0 8px;
						height: 17px;
						color: #fff;
						font-size: 9px;
						text-align: center;
						line-height: 17px;
						background-color: rgba(217, 48, 48, .8);
						border-top-right-radius: 17px;
						border-bottom-right-radius: 17px;
					}

					.Isthd_num {
						position: absolute;
						right: 2px;
						top: 0;
						z-index: 3;
						padding-left: 15px;
						color: #fff;
						font-size: 12px;
						background-position: 0;
						background-repeat: no-repeat;
						background-size: 11px 10px;
						text-shadow: 1px 0 0 rgba(0, 0, 0, .15);

						&::before {
							content: "";
							background: no-repeat url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMiAyMCI+PHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBmaWxsPSIjMDQwMDAwIiBkPSJNMjIgMTYuNzc3YzAgMS4yMzMtMS4xMjEgMi4yMzMtMi41MDYgMi4yMzMtMS4zODQgMC0yLjUwNi0xLTIuNTA2LTIuMjMzdi0yLjU1M2MwLTEuMjM0IDEuMTIyLTIuMjMzIDIuNTA2LTIuMjMzLjE3NCAwIC4zNDMuMDE3LjUwNi4wNDZ2LTEuMzdoLS4wMzNjLjAxNy0uMjIuMDMzLS40NDEuMDMzLS42NjZhOCA4IDAgMCAwLTE2IDBjMCAuMjI1LjAxNi40NDYuMDM0LjY2Nkg0djEuMzdjLjE2My0uMDI5LjMzMy0uMDQ2LjUwNS0uMDQ2IDEuMzg0IDAgMi41MDYuOTk5IDIuNTA2IDIuMjMzdjIuNTUzYzAgMS4yMzMtMS4xMjIgMi4yMzMtMi41MDYgMi4yMzNTMiAxOC4wMTEgMiAxNi43Nzd2LTIuNTUzYzAtLjI1OC4wNTktLjUwMS4xNDgtLjczQS45ODIuOTgyIDAgMCAxIDIgMTMuMDAxdi0yLjY2N2MwLS4wMjMuMDEyLS4wNDMuMDEzLS4wNjctLjAwNC0uMDg4LS4wMTMtLjE3Ni0uMDEzLS4yNjYgMC01LjUyMyA0LjQ3Ny0xMCAxMC0xMHMxMCA0LjQ3NyAxMCAxMGMwIC4wOS0uMDA5LjE3OC0uMDE0LjI2Ni4wMDIuMDI0LjAxNC4wNDQuMDE0LjA2N3YyYS45ODguOTg4IDAgMCAxLS4zNi43NTNjLjIyNC4zMzQuMzYuNzIuMzYgMS4xMzh2Mi41NTIiIG9wYWNpdHk9Ii4xNSIvPjxwYXRoIGZpbGwtcnVsZT0iZXZlbm9kZCIgZmlsbD0iI2ZmZiIgZD0iTTIwIDE2Ljc3N2MwIDEuMjMzLTEuMTIxIDIuMjMzLTIuNTA2IDIuMjMzLTEuMzg0IDAtMi41MDYtMS0yLjUwNi0yLjIzM3YtMi41NTNjMC0xLjIzNCAxLjEyMi0yLjIzMyAyLjUwNi0yLjIzMy4xNzQgMCAuMzQzLjAxNy41MDYuMDQ2di0xLjM3aC0uMDMzYy4wMTctLjIyLjAzMy0uNDQxLjAzMy0uNjY2YTggOCAwIDAgMC0xNiAwYzAgLjIyNS4wMTYuNDQ2LjAzNC42NjZIMnYxLjM3Yy4xNjMtLjAyOS4zMzMtLjA0Ni41MDUtLjA0NiAxLjM4NCAwIDIuNTA2Ljk5OSAyLjUwNiAyLjIzM3YyLjU1M2MwIDEuMjMzLTEuMTIyIDIuMjMzLTIuNTA2IDIuMjMzUzAgMTguMDExIDAgMTYuNzc3di0yLjU1M2MwLS4yNTguMDU5LS41MDEuMTQ4LS43M0EuOTgyLjk4MiAwIDAgMSAwIDEzLjAwMXYtMi42NjdjMC0uMDIzLjAxMi0uMDQzLjAxMy0uMDY3LS4wMDQtLjA4OC0uMDEzLS4xNzYtLjAxMy0uMjY2IDAtNS41MjMgNC40NzctMTAgMTAtMTBzMTAgNC40NzcgMTAgMTBjMCAuMDktLjAwOS4xNzgtLjAxNC4yNjYuMDAyLjAyNC4wMTQuMDQ0LjAxNC4wNjd2MmEuOTg4Ljk4OCAwIDAgMS0uMzYuNzUzYy4yMjQuMzM0LjM2LjcyLjM2IDEuMTM4djIuNTUyIi8+PC9zdmc+");
							background-position: left center;
							background-size: auto 100%;
							width: 1.2em;
							height: 0.9em;
							display: inline-block;
						}
					}
				}

				.plhead_writter {
					-webkit-box-flex: 1;
					flex: 1 1 auto;
					width: 1%;
					margin-left: 16px;
					font: 14px/1.5 Helvetica, sans-serif, STHeiTi;

					.thind {
						padding-top: 1px;
						font-size: 17px;
						line-height: 1.3;
						color: #fefefe;
						height: 44px;
						display: -webkit-box;
						-webkit-box-pack: center;
					}

					.avater {
						display: block;
						position: relative;
						margin-top: 20px;

						.p_avater {
							line-height: 1.3;
							color: hsla(0, 0%, 100%, .7);
						}
					}
				}
			}

			// .middlebottom {
			// 	width: 100%;
			// 	height: 100px;
			// 	background-color: skyblue;
			// 	position: relative;
			// 	z-index: 2;
			// }
		}
	}
</style>
