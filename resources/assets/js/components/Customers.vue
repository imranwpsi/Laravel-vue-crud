<template>          
  <table class="table table-bordered">
    <thead>
      <tr>
        <th>Name</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody>
      <customer v-for="customer in customers" v-bind:customer="customer"></customer>
    </tbody>
  </table>     
</template>

<script>
    import customer from './Customer.vue';
    export default {
        data(){
        	return{
        		customers: [
        			// {name:'Imran Hossain',email:'imran@gmail.com'},
        			// {name:'Emon',email:'emon@gmail.com'}
        		],
        	}
        },
        components:{customer},
        created(){
        	this.fetchCustomer();
        },
        methods:{
        	fetchCustomer(){
        		this.$http.get("customer").then(response => {this.customers = response.data.customers});
        	}
        }
    }
</script>