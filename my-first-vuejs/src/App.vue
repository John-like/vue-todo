<template>
  <div id="app">
   <h1 v-html="title"></h1>
   
   <input type="text" v-model='newitem' v-on:keyup.enter="addNew"/>
   <ul>
	   	<li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">
	   		{{item.label}}
	   	</li>	
   </ul>
   <p>{{newitem}}</p>
  </div>
</template>

<script>
import Store from './export.js'
console.log(Store)	

export default {
	  data:function(){
	  	return{
	  		title:"<p>vuestudy</p>",
	  		items:[
	  		],
	  		newitem:'',
	  	
	  		
	  	}
	  },
	  watch:{
	  	items:{
	  		handler:function(items){
	  			console.log(items)
	  			Store.save(items)
	  		},
	  		deep:true
	  	}
	  },
	  methods:{
	  	toggleFinish:function(item){
	  			item.isFinished=!item.isFinished;
	  	},
	  	addNew:function(){
	  		this.items.push({
	  			label:this.newitem,
	  			isFinished:true
	  		})
	  	
	  		//alert(this.newitem)
	  		this.newitem='';
	  	}
	  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished{
	text-decoration: underline;
	color: red;
}
.liClass{
	color: red;
}
.class2{
	font-size: 20px;
}
</style>
