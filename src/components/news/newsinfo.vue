<template>
	<div id='tmpl'>
	<div class='title'>
		<h4 v-text='info.title'>标题</h4>
		<p>{{info.add_time | datefmt('YYYY MM DD')}} {{info.click}}次浏览量</p>
	</div>
	<div id='content' v-html='info.content'>
		内容

	</div>


	</div>

</template>

<script>
   import common from '../../kits/common.js';
	export default{
     data(){
     	return {
     		id:0,  //传入的id值
     		info:{
     			   /*"id":13,
     			   "title":"1季度多家房企利润跌幅超50% 去库存促销战打响",
     			   "click":1,
     			   "add_time":"2015-04-16T03:50:28.000Z",
     			   "content"*/
     		}
     	}
     },
     created(){
     	// 1.0获取url传入的id参数赋值给data中的id属性
     	 this.id=this.$route.params.id;

     	 //2.0请求服务器获取到这个id对应的详情数据对象
     	       this.getinfo();
     },
    methods:{
    	getinfo(){
    		//1.0 定义url
    		var url=common.apidomain+ '/api/getnew/'+this.id;
    		//2.0发出ajax请求获取数据
    		this.$http.get(url).then(function(res){
    			var body=res.body;
    			if(body.status!=0){
                       	alert(body.message);
                       	return;
                       }
                   //3.0赋值
                   this.info=body.message[0];    
    		})
    	}
    }
 }

</script>

<style scoped>
	.title h4{
		color: #0094ff;
	}
	.title p{
		color: rgba(0,0,0,0.5);
	}
	.title,#content{
		padding: 5px;
	}

</style>
