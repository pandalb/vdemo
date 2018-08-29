<template>
	<div class="manage tc">
		<button @click="add">新增</button>
		<div class="input-area" v-show="showAdd">
			<input type="text" placeholder="请输入人员姓名" v-model="nameValue">
			<button @click="addName">确定</button>
		</div>
		<table>
			<tr>
				<th>姓名</th>
				<th>操作</th>
			</tr>
			<tr v-for='(item,index) in peoples'>
				<td>
					{{item.name}}
				</td>
				<td :id="index">
					<span @click='edit'>编辑</span>
					<span @click='del'>删除</span>
				</td>
			</tr>
		</table>
		<div class="wrap" v-show="showEdit">
			<div class="content">
				<input type="text" placeholder="请输入新名字" v-model="newName">
				<button @click="cancel">取消</button>
				<button @click="editName">确定</button>
			</div>
		</div>
		<footer-nav :class="{'isManage':isNowPage}"></footer-nav>
	</div>
</template>
<style >
	.manage button{border:0px;outline:none;height: 40px;border-radius: 10px;background-color: #41B883;color: #fff;font-size: 15px;}
	.manage button:first-child{width: 200px;height: 40px;}
	.input-area{margin-top: 10px;}
	.input-area input{width: 200px;height: 40px;outline:none;border:1px solid ##75878D;}
	.manage button:last-child{width: 50px;margin-left: 20px;}
	table{width: 100%;margin-top: 30px;font-size: 15px;}
	table tr{width: 100%}
	table tr td{width:50%;height: 20px;}
	.wrap{background-color: rgba(0,0,0,0.5);z-index:9;position:absolute;width: 100%;height: 100%;left: 0;top: 0;}
	.wrap .content{margin:250px auto;width: 250px}
	.wrap .content input{width: 200px;height: 50px;display: block;margin: 10px auto}
	.wrap .content button{width: 100px;height:50px;}
</style>
<script>
	import FooterNav from '../../components/footer.vue';
	export default{
		components:{
			FooterNav
		},
		data(){
			return{
				isNowPage:true,
				showAdd:false,
				showEdit:false,
				peoples:[{'name':'jack'},{'name':'joy'}],
				nameValue:'',
				newName:'',
				editId:0
			}
		},
		methods:{
			add(){
				this.showAdd=true
			},
			addName(){
				var v=this.nameValue
				if(v.trim()==''){
					alert("请输入新增人员姓名！")
				}else{
					var data={}
					data.name=v
					this.peoples.push(data)
					this.nameValue=''
					this.showAdd=false
				}
			},
			del(e){
				var id=e.target.offsetParent.id
				this.peoples.splice(id,1)
			},
			edit(e){
				var id=e.target.offsetParent.id
				this.showEdit=true
				this.editId=id
				this.newName=this.peoples[id].name
			},
			cancel(){
				this.showEdit=false
			},
			editName(){
				var v=this.newName
				if(v.trim()==''){
					alert("请输入姓名！")
				}else{
					this.peoples[this.editId].name=this.newName
					this.showEdit=false
				}
			}
		}
	}
</script>