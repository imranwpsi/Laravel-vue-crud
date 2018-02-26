<template>
	<tr>
	  	<td>
	  		<input type="text" v-model="editForm.name" class="form-control" v-if="edit">
	  		<span v-else>{{ customer.name }}</span>
	  	</td>
	  	<td>
	  		<input type="text" v-model="editForm.email" class="form-control" v-if="edit">
	  		<span v-else>{{ customer.email }}</span>
		</td>
	  	<td>
	  		<button type="button" class="btn btn-info btn-xs" v-on:click="editCustomer" v-if="!edit">Edit</button>
	  		<button type="button" class="btn btn-default btn-xs" v-on:click="cancelEdit" v-if="edit">Cancel</button>
	  		<button type="button" class="btn btn-danger btn-xs" v-on:click="$emit('delete-customer',customer)" >Delete</button>
	  	</td>
	</tr>
</template>

<script>
	export default{
		props:['customer'],

		data(){
			return{
				edit:false,
				editForm:{
					name:'',
					email:'',
				}
			}
		},

		methods:{
			editCustomer(){
				this.edit=true;
				this.editForm.name=this.customer.name;
				this.editForm.email=this.customer.email;
			},
			cancelEdit(){
				this.edit=false;
				this.editForm.name='';
				this.editForm.email='';
			}
		}

	}
</script>