<template>
  <div id="app">
	<!-- header -->
   <app-header :poiInfo="poiInfo"></app-header>
   <!-- nav -->
   <app-nav :commentNum="commentNum"></app-nav>
   <!-- content -->
   <router-view></router-view>
  </div>
</template>

<script>
import Header from './components/header/Header.vue'
import Nav from './components/nav/Nav'
export default {
  name: 'App',
  data(){
	  return{
		  poiInfo:{},
		  commentNum:0
	  }
  },
  components: {
     "app-header":Header,
	 "app-nav":Nav
  },
  created(){
	  //fetch
	  fetch("/api/goods")
	   .then(res=>{
		   return res.json()
	   })
	   .then(response =>{
		   // console.log(response)
		   if(response.code==0){
			   this.poiInfo = response.data.poi_info;
		   }
	   })
	   // 请求ratings
	   fetch("/api/ratings")
	    .then(res=>{
	   		   return res.json()
	    })
	    .then(response =>{
	   		   // console.log(response)
	   		   if(response.code==0){
	   			   this.commentNum = response.data.comment_num;
	   		   }
	    })
  }
}
</script>

<style>

</style>
