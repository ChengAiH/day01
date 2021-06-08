<template>
	<li 
	class="itemes"
	v-on:click="Upload"
	
	>{{iteme.first}}</li>
</template>
<!-- v-if="!suggests.length && !inputing && !inputValue" -->
<script>
	export default{
		props:["iteme","inputValue","inputing"],
		methods:{
			Upload:function(){
				this.$emit("update:music",this.inputValue = this.iteme.first)
			}
		}
	}
</script>

<style lang="less">
	.itemes{
		display: inline-block;
		height: 32px;
		margin: 10px 0 8px 8px;
		padding: 0 14px;
		font-size: 14px;
		line-height: 29px;
		color: #333;
		border-width: 1px;
		border-color: #d3d4da;
		border-radius: 32px;
		border: 1px solid rgba(0,0,0,.1);
		transform-origin: top left;
		box-sizing: border-box;
	}
</style>
