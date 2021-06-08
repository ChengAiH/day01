<template>
	<div class="hot">
		<hotTop></hotTop>
		<hotbottom 
		@update:music="$emit('update:music', $event)" 
		:Hotsongrecommendation="$attrs.Hotsongrecommendation"
		:HotbottomSong="HotbottomSong"
		:paused="$attrs.paused"
		:currentMusic="$attrs.currentMusic"
		></hotbottom>
	</div>
</template>
<script>
	import hotTop from "@/components/hotTop.vue"
	import hotbottom from "@/components/hotbottom.vue"

	export default {
		created() {
			// console.log("Hot created");
			this.$root.isShowLoading = true;
			this.axios
				.get("/top/list?idx=1")
				.then((response) => {
					this.$root.isShowLoading = true;
					this.axios
						.get(
							"/song/detail?ids=" +
							response.data.playlist.trackIds
							.slice(0, 20)
							.map((e) => e.id)
							.join()
						)
						.then((response) => {
							console.log(response)
							this.HotbottomSong=response.data.songs;
						})
						.finally(() => {
							this.$root.isShowLoading = false;
						});
				})
				.finally(() => {
					this.$root.isShowLoading = false;
				});
		},
		components: {
			hotTop,
			hotbottom,
		},
		data: function() {
			return {
				Hotsongrecommendation: [],
				HotbottomSong:{},
			};
		},
		computed: {
			currentRecommends: function() {
				return this.recommends.slice(0, 6);
			},
		},
		// created(){
		// 	this.axios.get("/top/list?idx=1").then((response) => {
		// 	  console.log(response);
		// 	  // this.recommends = response.data.result;
		// 	});
		// }
	};
</script>

<style>
</style>
