<template>
	<ul>
		<Hotbottomsong
		v-for="songsok in HotbottomSong"
		:key="songsok.id"
		:songsok="songsok"
		:HotbottomSong="HotbottomSong"
		></Hotbottomsong>
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
		components:{
			Hotbottomsong,
		}
	}
</script>

<style lang="less">
</style>
