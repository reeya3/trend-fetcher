<template>
 <div>
 	<p v-text="dropdownresult">Selected</p>
 	<dropdown  @update-option="optionUpdate"> </dropdown>

<img src="https://media.giphy.com/media/N256GFy1u6M6Y/giphy.gif" v-if="loader">

 	<ol v-else>

 		<li v-for="item in items" >
 			
 				<h3>Name:{{item.full_name}}</h3>
 					<h3>Id:{{item.id}}</h3>
 					<a :href= "item.clone_url">CLONE URL :{{item.clone_url}}</a>
 						<a :href="item.clone_url" target="_blank"> 
 							<img :src="item.owner.avatar_url" width="100px" height="100px" align="right"  target="_blank"/></a>



 			
 		</li>
 	</ol>


 </div>



	
</template>
<script>
	import Dropdown from './Dropdown.vue';
	import axios from 'axios';

export default{

	components: {

		Dropdown,
	},
	data(){
		return {
			dropdownresult: '',
			items: [],
			loader: false,
		};
	},
	methods:{
		optionUpdate(value){
			this.dropdownresult = value;
			this.loader= true,
			axios.get(`https://api.github.com/search/repositories?q=stars:>1+language:${value}&sort=stars&order=desc&type=Repositories`)
			.then(response => {
				debugger
				console.log(response)
				this.loader = false,
				this.items = response.data.items;

			});

		},
	}
}
</script>