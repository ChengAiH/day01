<template>
	<div class="search">
		<form>
			<div class="inputcover">
				<i class="icon"></i>
				<input 
					type="search" 
					placeholder="搜索歌曲、歌手、专辑" 
					@input="worldinput"
					@keyup="inputing = false"
					v-model.trim="inputValue"
				>
			</div>
		</form>

		<div class="popular">
			<section class="m-hot">
				<h3 class="onetitle">热门搜索</h3>
				<ul class="ulli" v-if="!suggests.length && !inputing && !inputValue">
					
					<div
					v-for="(itemes,index) in searchdata"
					:key="index"
					@click="oko(inputValue)"
					>
					<li class="itemes"
					v-if="!suggests.length && !inputing && !inputValue"
					@click="inputValue = itemes.first"
					>{{itemes.first}}</li>
					</div>
					
				</ul>
				<!-- 热门搜索 -->
				<ul v-if="!inputing && inputValue" class="eight">
				<li 
					v-for="(item,index) in suggests"
					:key="index"
					@click="Playhot({item:item,index})"
				>
					<p class="double">{{item.name}}123</p>
					<span class="doubletwo"
						v-for="(itema,index) in item.artists"
						:key="index"
					>{{itema.name}}</span>-
					<span class="doubletwo">{{item.album.name}}</span>
					<div class="icond">
						<span
							class="playing"
							:class="{ paused: paused }"
							v-if="currentMusic && currentMusic.id === item.id"
						>
							<i></i>
							<i></i>
							<i></i>
						</span>
						<span class="Playicon" v-else>▶</span>
					</div>
				</li>
				</ul>
				<ul v-if="inputing && suggests.length" class="eight">
					<li
						v-for="(item, index) in suggests"
						:key="index"
						@click="Playsus({item:item,index})"
					>
					
						<p class="double">{{item.name}}</p>
						<span class="doubletwo"
							v-for="(itema,index) in item.artists"
							:key="index"
						>{{itema.name}}</span>-
						<span class="doubletwo">{{item.album.name}}</span>
						<div class="icond">
							<span
								class="playing"
								:class="{ paused: paused }"
								v-if="currentMusic && currentMusic.id === item.id"
							>
								<i></i>
								<i></i>
								<i></i>
							</span>
							<span class="Playicon" v-else>▶</span>
						</div>
					</li>
					
				</ul>
			</section>
		</div>
		<Searchbox
			v-if="!suggests.length && !inputing && !inputValue"
			:todos="todos"
			@deleteTodo="$emit('delete-todo', $event)"
			@todname="todaname"
		></Searchbox>
	</div>
		
</template>

<script>
	import Searchbox from "@/components/Searchbox.vue"	
	export default {
		props:["currentMusic","paused"],
		components: {
			Searchbox,
		},
		data: function() {
			return {
				searchdata: [],
				inputValue: "",
				suggests: [],
				inputing: false,
				todos:[],
			};
		},
		created() {
			this.axios.get("/search/hot").then((response) => {
				this.searchdata = response.data.result.hots;
			});
		},
		methods:{
			inputed:function(){
				this.inputing = true;
				this.$emit("update:muise",this.inputing)
			},
			Playhot: function(songing) {
				this.$emit('update:music', songing)
			},
			Playsus:function(songing){
				this.$emit('update:music', songing)
			},
			worldinput:function(){
				this.inputing = false
				console.log(this.inputValue)
			},
			oko:function(inputValue){
				this.inputing = true
				this.todos.push({
					inputValue,
					id: this.todos.length ? this.todos[this.todos.length - 1].id + 1 : 0,
				})
			},
			// 删除元素
			deleteTodo: function (id) {
				console.log("deleteTodo", id);
				// this.todos = this.todos.filter((todo) => {
				// 	return todo.id !== id;
				// });
			},
			todaname:function(name){
				this.inputValue = name
			}
		},
		watch: {
			inputValue: function(n) {
				if (n) {
					if (this.inputing) {
						this.axios
							.get("/search?keywords=" + n)
							.then((res) => {
								// console.log(this.inputing)
								this.suggests = res.data.result.songs;
								console.log("搜索建议111", res.data.result.songs);
							});
					} else {
						this.axios
							.get("/search?keywords=" + n)
							.then((res) => {
								this.suggests = res.data.result.songs;
								console.log("123",this.suggests)
							});
					}
				} else {
					this.inputing = false;
					this.suggests = [];
				}
			},
		},
	}
</script>

<style lang="less">
	form {
		position: relative;
		padding: 15px 10px;

		.inputcover {
			position: relative;
			width: 100%;
			height: 30px;
			padding: 0 30px;
			box-sizing: border-box;
			background: #ebecec;
			border-radius: 30px;

			.icon {
				width: 13px;
				height: 13px;
				position: absolute;
				left: 0;
				top: 9px;
				margin: 0 8px;
				vertical-align: middle;
				background: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNiAyNiI+PHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBmaWxsPSIjYzljOWNhIiBkPSJNMjUuMTgxIDIzLjUzNWwtMS40MTQgMS40MTQtNy4zMTUtNy4zMTRBOS45NjYgOS45NjYgMCAwIDEgMTAgMjBDNC40NzcgMjAgMCAxNS41MjMgMCAxMFM0LjQ3NyAwIDEwIDBzMTAgNC40NzcgMTAgMTBjMCAyLjM0Mi0uODExIDQuNDktMi4xNiA2LjE5NWw3LjM0MSA3LjM0ek0xMCAyYTggOCAwIDEgMCAwIDE2IDggOCAwIDAgMCAwLTE2eiIvPjwvc3ZnPg==);
			}
			.eight{
				li{
					height: 32px;
					margin: 10px 0 8px 8px;
					padding: 0 14px;
					font-size: 14px;
					line-height: 29px;
					color: #333;
					border-width: 1px;
					border-color: #d3d4da;
					transform-origin: top left;
				}
			}
			input {
				width: 100%;
				height: 30px;
				line-height: 18px;
				background: rgba(0, 0, 0, 0);
				font-size: 14px;
				color: #333;
				border-radius: 0;
				border: 0;
				font: 14px/1.5 Helvetica, sans-serif, STHeiTi;
				outline: 0;
			}
		}
	}
	.popular {
		.m-hot {
			h3 {
				font-size: 12px;
				line-height: 12px;
				color: #666;
				font-weight: 400;
				padding-left: 10px;
			}
			.ulli{
				// float: left;
				margin-bottom: 15px;
				div{
					display: inline-block;
					height: 32px;
					margin-right: 8px;
					margin-bottom: 15px;
					// padding: 0 14px;
					font-size: 14px;
					line-height: 32px;
					color: #333;
				}
			}
			.eight{
				li{
					height: 32px;
					margin: 0px 0px 45px 8px;
					padding: 0 14px;
					font-size: 14px;
					line-height: 29px;
					color: #333;
					border-width: 1px;
					border-color: #d3d4da;
					transform-origin: top left;
					.double{
						font-size: 17px;
					}
					
					.icond {
						width: 30px;
						height: 30px;
						float: right;
						margin-top: -20px;
						.Playicon{
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
							transform-origin: center bottom;
							animation: playing 0.6s linear -0.2s infinite alternate-reverse;						
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
				
			}
			ul {
				// float: left;
				padding: 10px 0 0 10px;
				div{
					// float: left;
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
				}
				
			}
		}
	}
	
</style>

