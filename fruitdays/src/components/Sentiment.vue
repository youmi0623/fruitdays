<template>
	<div>
		<div class="Sentiment-top">
			<img src="../assets/img/sectionRenqi.jpg"/>
		</div>
		<router-link :to="{name : 'Detail',params:{fid: item.target_id}}" class="goods" v-for="item in goodlist" :key="item.id">
			<div class="goodimg">
				<img  v-lazy="item.image"/>
			</div>
			<div class="goods-list">
				<h2>{{item.title}}</h2>
				<p>{{item.subtitle}}</p>
				<div class="sprice">
					<span>￥{{item.price}} / </span>
					<em>{{item.volume}}</em>
					<i class="iconfont   icon-jiahao"></i>
				</div>
			</div>
		</router-link>
	</div>
</template>

<script>
import { Lazyload } from 'mint-ui';	
import axios from 'axios';
export default{
	name : "mintui",
	data : function(){
		return {
			goodlist: [],
		}
	},
	mounted : function(){
		axios.get(`${this.$store.state.goodapi}`)
		  .then((response)=>{
		    console.log(response);
		    this.goodlist = response.data.data.banner.mainBanners[21].content
		  })
		  .catch(function (error) {
		    console.log(error);
		  });
	}
}
</script>

<style scoped>
.Sentiment-top{
	width: 100%;
	height: 64px;
}
.Sentiment-top img{
	width: 100%;
	height: 100%;
}
.goods{
	width: 375px;
	height: 160px;
	display: flex;
	justify-content: space-around;
	align-items: center;
}
.goodimg{
	width: 120px;
	height: 120px;
}
.goodimg img{
	width: 100%;
	height: 100%;
	min-height: 120px;
}
.goods-list{
	width: 193px;
	height: 105px;
}
h2{
	color: #3a3a3a;
    font-weight: 400;
    line-height: normal;
    margin-bottom: 10px;
}
.goods-list p{
	color: #878787;
    margin-bottom: 37px;
}
.sprice span{
	color: #ff8000;
    width: 100%;
    font-size: 18px;
    white-space: nowrap;
}
.sprice em{
	color: #ff8000;
    width: 100%;
    white-space: nowrap;
    font-style: normal;
}
.icon-jiahao{
	float: right;
	font-size: 22px!important;
	color: #ff8000;
}
</style>