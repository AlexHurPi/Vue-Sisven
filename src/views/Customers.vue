<template>
<div class="container"> 
    <h1 class="text-start">Customers List |   
        <button @click="newCustomer()"  
        class="btn btn-success mx-2">
        <font-awesome-icon icon="plus" />
        </button>
    </h1>  
    <table class="table">
    <thead>
        <tr>
            <th scope="col">#</th>
            <th scope="col">Id</th>
            <th scope="col">Document Number</th>
            <th scope="col">First Name</th>
            <th scope="col">Last Name</th>
            <th scope="col">Address</th>
            <th scope="col">Birthday</th>
            <th scope="col">Phone Number</th>
            <th scope="col">E-Mail</th> 
            <th scope="col">Actions</th>            
        </tr>
    </thead>
    <tbody>       
        <tr v-for="(customer,index) in customers" :key="index">
            <th scope="row">{{ index + 1 }}</th>
            <td>{{ customer.id }}</td>
            <td>{{ customer.document_number }}</td>
            <td>{{ customer.first_name }}</td>
            <td>{{ customer.last_name }}</td>
            <td>{{ customer.address }}</td>
            <td>{{ customer.birthday }}</td>
            <td>{{ customer.phone_number }}</td>
            <td>{{ customer.email }}</td>   
            <td>
                <button @click="deleteCustomer(customer.id)"
                   class="btn btn-danger mx-2">
                   <font-awesome-icon icon="trash" />
               </button> 
               <button @click="editCustomer(customer.id)"           
               class="bnt bnt-warning mx-2">
               <font-awesome-icon icon="pencil" />
            </button> 
            </td>
        </tr>       
    </tbody>
    </table>
    </div>   
</template>
<script>
import axios from 'axios'
import Swal from 'sweetalert2'

export default {

    name: 'Customer',
    data(){
        return{
            customers: []
        }
   },
   methods: {
       deleteCustomer(id){
           Swal.fire({
              title: `Do you want to delete the Customer with id ${id}?`,
              showCancelButton: true,
              confirmButtonText: 'Delete',
              }).then((result) => {
              /* Read more about isConfirmed, isDenied below */
              if (result.isConfirmed) {
                 //Swal.fire('Saved!', '', 'success')
                 axios.delete(`http://127.0.0.1:8000/api/customers/${id}`)
                 .then(response => {
                     if (response.data.success){
                        Swal.fire('Deleted!! ', '', 'success')
                        this.customers = response.data.customers
                     }
                 })
               }
           })
    },
    editCustomer(id){
    this.$router.push({name: 'EditarCustomer', params: { id: `${id}` }} )
},
newCustomer(){
    this.$router.push({name: 'NewCustomer'});
}
},
mounted() {
    axios
        .get('http://127.0.0.1:8000/api/customers')
        .then(response => (this.customers = response.data.customers.data))
},
}