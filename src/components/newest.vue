<template>
	<div class="new_ous">
		<div class="new_top">
			<p class="commenting">更新评论</p>
		</div>
		<div class="new_bottom">
			
			<div class="new_bottom_middle">
				<ul
				v-for="(item,index) in aggregatetwo"
				:key="index"
				>
					<li>
						<div class="p_four"><a href="javascript"><img :src="item.user.avatarUrl"></a></div>
						<div class="p_one">
							<!-- <span><a href="javascript"><img :src="item.user.avatarUrl"></a></span> -->
							<div class="oneof">
							<span class="span_one">{{item.user.nickname}}</span>
							<span class="span_two">
								<span>{{item.likedCount}}</span>
								<i class="cmt"><svg class="u-svg u-svg-unzancmt" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 28 28"><path fill="#999" d="m25.857 14.752c-.015.059-1.506 5.867-2.932 8.813-1.162 2.402-3 2.436-3.099 2.436h-12.826v-13c3 0 5.728-4 5.728-7.275 0-3.725 1.433-3.725 2.142-3.725 1.327 0 1.978 1.345 1.978 4 0 2.872-.832 4.525-.839 4.537-.161.31-.155.682.027.981.181.299.5.482.849.482h6.942c.922 0 1.551.215 1.866.64.467.626.286 1.705.164 2.112m-23.857 10.248v-10c0-1.795.659-1.981.855-2h2.145v13h-2.173c-.829 0-.827-.648-.827-1m25.309-13.54c-.713-.969-1.886-1.46-3.482-1.46h-5.519c.26-.932.519-2.285.519-4 0-5.221-2.507-6-4-6-1.909 0-4.185.993-4.185 5.725 0 2.206-1.923 5.275-3.815 5.275h-4-.011c-1.034.011-2.816.862-2.816 4v10.02c0 1.198.675 2.979 2.827 2.979h16.971.035c.364 0 3.224-.113 4.894-3.564 1.514-3.127 3.01-8.942 3.056-9.14.071-.23.664-2.289-.474-3.836"></path></svg></i>
							</span>
							</div>
							<div class="twoof">
								<p class="pthree">{{item.content}}</p>
							</div>
						</div>
						<p class="p_two"></p>
						
					</li>
				</ul>
				
			</div>
			
		</div>
	</div>
	
</template>

<script>
	export default{
		props:["aggregatetwo"]
	}
</script>

<style lang="less">
	.new_ous{
		.new_top{
			.commenting{
				padding: 0 10px;
				height: 23px;
				line-height: 23px;
				margin: 0;
				color: #666;
				font-size: 12px;
				font-weight: 400;
				background: rgba(0,0,0,.05);
			}
		}
		.new_bottom{
			.new_bottom_middle{
				
				ul{
					padding-top: 20px;
					margin: 0 10px;
					li{
						display: flex;
						.p_four{
							flex: 1;
							img{
								display: block;
								border-radius: 50%;
								width: 30px;
								height: 30px;
							}
						}
						.p_one{
							flex: 9;
							display: inline-block;
							.oneof{
								.span_one{
									display: block;
									// float: left;
									font-size: 15px;
									color: #666;
								}
								.span_two{
									
									float: right;
									span{
										display: inline-block;
										min-width: 30px;
										padding-left: 15px;
										font-size: 11px;
										color: #999;
									}
									.cmt{
										display: inline-block;
										width: 14px;
										height: 14px;
										margin-left: 6px;
										line-height: 0;
										vertical-align: middle;
									}
								}
							}
							.twoof{
								margin-top: 10px;
								width: 85%;
								.p_three{
									font-size: 15px;
									color: #333;
								}
							}
						}
					}
				}
			}
		}
	}
</style>
