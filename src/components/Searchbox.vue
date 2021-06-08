<template>
	<div class="inputcover">
		<ul
			v-for="(list,index) in todos"
			:key="index"
			@click="$emit('todname',list.inputValue)"
		>
			<li
			>
				<span class="todos_first"></span>
				<span class="todos_second">{{list.inputValue}}</span>
				<span class="todos_third" 
				@click="deletes(list.id)"
				></span>
			</li>
		</ul>
	</div>
</template>

<script>
	export default {
		props:["todos"],
		methods:{
			
			// deletes:function(todo){
			// 	this.$emit('delete-todo', todo)
			// 	// console.log(todo)
			// },
		}
	}
</script>

<style lang="less">
	.inputcover{
		ul{
			li{
				display: flex;
				align-items: center;
				height: 45px;
				.todos_first{
					margin: 0 10px;
					width: 15px;
					height: 15px;
					background-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAzMCAzMCI+PHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBmaWxsPSIjYzljYWNhIiBkPSJNMTUgMzBDNi43MTYgMzAgMCAyMy4yODQgMCAxNVM2LjcxNiAwIDE1IDBzMTUgNi43MTYgMTUgMTUtNi43MTYgMTUtMTUgMTVtMC0yOEM3LjgyIDIgMiA3LjgyIDIgMTVzNS44MiAxMyAxMyAxMyAxMy01LjgyIDEzLTEzUzIyLjE4IDIgMTUgMm03IDE2aC04YTEgMSAwIDAgMS0xLTFWN2ExIDEgMCAxIDEgMiAwdjloN2ExIDEgMCAxIDEgMCAyIi8+PC9zdmc+);
					display: inline-block;
					vertical-align: middle;
					background-position: 0 0;
					background-size: contain;
					background-repeat: no-repeat;
				}
				.todos_second{
					flex: 1;
				}
				.todos_third{
					float: right;
					margin: 0 20px;
					width: 12px;
					height: 12px;
					background-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBmaWxsPSIjOTk5ODk5IiBkPSJNMTMuMzc5IDEybDEwLjMzOCAxMC4zMzdhLjk3NS45NzUgMCAxIDEtMS4zNzggMS4zNzlMMTIuMDAxIDEzLjM3OCAxLjY2MyAyMy43MTZhLjk3NC45NzQgMCAxIDEtMS4zNzgtMS4zNzlMMTAuNjIzIDEyIC4yODUgMS42NjJBLjk3NC45NzQgMCAxIDEgMS42NjMuMjg0bDEwLjMzOCAxMC4zMzhMMjIuMzM5LjI4NGEuOTc0Ljk3NCAwIDEgMSAxLjM3OCAxLjM3OEwxMy4zNzkgMTIiLz48L3N2Zz4=);
					display: inline-block;
					vertical-align: middle;
					background-position: 0 0;
					background-size: contain;
					background-repeat: no-repeat;
				}
			}
		}
	}
</style>
