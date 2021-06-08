<template>
		<li
		:style="{
			'font-size':index==currentRow?'1.3rem':'.9rem',
			'color':index==currentRow?'white':'rgba(255,255,255,0.5)',
		}"
		>
		<span>{{truelyric.text}}</span>
		
		</li>
	
</template>

<script>
	export default{
		props:["Reallylyric","truelyric","index","currentTime"],
		data: function() {
			return {
				currentRow:0,
				lyricMove:100
			};
		},
	}
</script>

<style lang="less">
</style>
