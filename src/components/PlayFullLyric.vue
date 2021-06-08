<template>
	<div class="lyric_new" @click="$emit('toggle-show-lyric')">
		<ul class="lyricMove" :style="{marginTop:lyricMove}">
			<newlyric
			class="newlyric"
			v-for="(truelyric,index) in Reallylyric"
			:key="index"
			:index="index"
			:truelyric="truelyric"
			:Reallylyric="Reallylyric"
			v-bind:currentTime="currentTime"
			:style="{
				'font-size':index==currentRow?'1.3rem':'.9rem',
				'color':index==currentRow?'white':'rgba(255,255,255,0.5)',
			}"
			>
			</newlyric>
		</ul>
	</div>
</template>

<script>
	import newlyric from "@/components/newlyric.vue";
	export default {
		props: ["currentMusic","currentTime"],
		data: function() {
			return {
				newlyric: [],
				Reallylyric:[],
				currentRow:0,
				lyricMove:100
			};
		},
		components:{
			newlyric,
		},
		created() {
			this.axios
				.get("/lyric?id=" + this.currentMusic.id)
				.then((response) => {
					this.newlyric = response.data.lrc.lyric;
					this.paresLyric(this.newlyric)
					this.Reallylyric = this.paresLyric(this.newlyric)
					// console.log(this.Reallylyric)
				})
		},
		watch:{
			currentTime:function(){
				this.Reallylyric.forEach((element,index)=>{
					// 比较我们歌词属性里的时间与当前播放时间，来定位到该歌词
					if(this.currentTime>element.time){
						this.lyricMove=-(index)*30+100+'px';
						this.currentRow=index;
						// this.propl = this.lyricMove;
						// return this.propl;
					}
				});
				
			}
		},
		methods: {
			paresLyric:function(lyric) {
				var patt = /\[\d{2}:\d{2}\.\d{2,3}\]/gi;
				var arr = lyric
					.split("\n")
					.filter((e) => e)
					.map((str) => {
						var time = str.match(patt)[0].replace(/(\[|\])/gi, "");
						var timeArr = time.split(":");
						time = Number(timeArr[0]) * 60 + Number(timeArr[1]);
						var text = str.replace(patt, "");
						return {
							time,
							text
						};
					});
				return arr;
			},
		},
	}
</script>

<style>
	.lyric_new{
		height: 380px;
		margin-top: 30px;
		overflow: hidden;
	}
	.lyricMove{
		color: white;
		text-align: center;
		line-height: 37px;
		margin-top: 60px;
	}
</style>
