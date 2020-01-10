<template>
		<select name="dropdown" id="dropdown"  v-on:change="optionchanged">
			<option value="null" disabled="">select any one</option>
			<option value="c">c</option>
			<option value="c++">c++</option>
			<option value="java">java</option>
			<option value="matlab">matlab</option>
	</select>
	

</template>

<script>
	export default{
		name: "Dropdown",

		data(){
			return{
				change: null,
			}

		},

		methods: {

			optionchanged(e){
				this.$emit('update-option',e.target.value);
			}


		}





	}

</script>