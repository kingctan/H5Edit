<template>
	<div class="dialog_con" v-show="showCreate" transition="fade">
		<div class="dialog_bg" @click="this.showCreate = false"></div>
		<div class="dialog_main_con small all_center">
			<div class="dialog_head">
				<h2>创建新作品</h2>
				<a href="javascript:void(0)" class="dialog_link close" @click="this.showCreate = false">&times;</a>
			</div>
			<div class="dialog_main">
				<div class="create_con all_center">
					<input type="text" placeholder="请输入作品标题" v-model="title"></input>
				</div>
			</div>
			<div class="dialog_bottom">
				<ul class="dialog_btn">
					<li @click="this.showCreate = false">取消</li>
					<li @click="submit">创建</li>
				</ul>
			</div>
		</div>
	</div>
</template>
<script>
	module.exports = {
		data: function(){
			return {
				title: '',
			}
		},
		props: ['showCreate'],
		methods: {
			submit: function(){
				var self = this;
				$.ajax({
					url: '/api/work/create',
					type: 'get',
					data:{
						title: self.title
					},
					success: function(data){
						var id = data.data._id;
						self.$route.router.go('/edit/' + id);
					}
				})
			}
		}
	};
</script>
<style>
	.create_con input{
		width: 330px;
		height: 36px;
		font-size: 12px;
		padding: 0 10px;
		line-height: 36px;
		display: block;
		border-radius: 6px;
		outline: 0;
		border: 1px solid #ddd;
	}
</style>