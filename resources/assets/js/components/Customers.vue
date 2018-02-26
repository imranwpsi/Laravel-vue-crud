<template>
    <div>
        <form v-on:submit.prevent="createCustomer" method="post">
            <div v-bind:class="{ 'form-group' : true, 'has-error' : errors.name }">
                <label for="name">Name</label>
                <input type="text" v-model="customer.name" class="form-control" id="name">
                <span class="help-block" v-for="error in errors.name" v-text="error"></span>
            </div>
            <div v-bind:class="{ 'form-group' : true, 'has-error' : errors.email }">
                <label for="name">Email</label>
                <input type="email" v-model="customer.email" class="form-control" id="email">
                <span class="help-block" v-for="error in errors.email" v-text="error"></span>
            </div>
            <div class="form-group">
                <input type="submit" class="btn btn-primary" value="Create New Customer">
            </div>
        </form>         
        <table class="table table-bordered">
            <thead>
              <tr>
                <th>Name</th>
                <th>Email</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody>
              <customer v-for="customer in customers" v-bind:customer="customer" v-on:delete-customer="deleteCustomer"></customer>
            </tbody>
        </table>
    </div>    
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
                errors:[],
                customer: {
                    name:'',
                    email:''
                }
        	}
        },

        components:{ customer },

        created(){
        	this.fetchCustomer();
        },

        methods:{
        	fetchCustomer(){
        		this.$http.get("customer").then(response => {this.customers = response.data.customers});
        	},
            createCustomer(){
                this.$http.post("/customer/",this.customer).then(response => {
                    this.customers.push(response.data.customer);
                    this.customer={name:'',email:''};
                    if(this.errors){
                        this.error=[];
                    }
                    console.log(response.data)
                },response =>{
                    this.errors=response.data.errors;
                });
            },
            deleteCustomer(customer){
                this.$http.delete("/customer/"+customer.id).then(response => {
                    let index = this.customers.indexOf(customer);
                    this.customers.splice(index,1);
                    console.log(response.data);
                });
            }
        }
    }
</script>