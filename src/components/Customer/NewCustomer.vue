<template>
    <div class="container text-start">
       <h1 class="text-primary fw-bold"> New</h1>
       <div class="card">
           <div class="card-header fw-bold">Customer</div>
      <div class="card-body">
          <form @submit.prevent="saveCustomer">
        
              <div class="row mb-3">
                
                <label for="id" class="form-label">Id</label>
                
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="tag" /></div>
                    <input type="text" class="form-control" id="id" 
                    placeholder="Id Customer" disabled v-model='customer.id'>
                </div>
             </div>
 
            <div class="row mb-3">                
                <label for="document_number" class="form-label">Document Namber : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="namec" placeholder="document_number" 
                       v-model='customer.document_number'>
                </div>
             </div>

             <div class="row mb-3">                
                <label for="first_name" class="form-label">First Name : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="first_name"
                     placeholder="First Name" v-model='customer.first_name'>
                </div>
             </div>   
             
             <div class="row mb-3">                
                <label for="last_name" class="form-label">Last Name : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="last_name"
                     placeholder="Last Name" v-model='customer.last_name'>
                </div>
             </div>             

             <div class="row mb-3">                
                <label for="address" class="form-label">Address : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="address"
                     placeholder="address" v-model='customer.address'>
                </div>
             </div>     
             
             <div class="row mb-3">                
                <label for="birthday" class="form-label">Birthday : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="birthday"
                     placeholder="Birthday" v-model='customer.birthday'>
                </div>
             </div>      

             <div class="row mb-3">                
                <label for="phone_number" class="form-label">Phone Number : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="phone_number"
                     placeholder="Phone Number" v-model='customer.phone_number'>
                </div>
             </div>      

             <div class="row mb-3">                
                <label for="email" class="form-label">E-Mail : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="email"
                     placeholder="E-Mail" v-model='customer.email'>
                </div>
             </div>     
     <button class="btn btn-primary" type="submit">Actualizar</button>
     <button class="btn btn-secondary mx-2" @click="cancelar">Cancelar</button>
    </form>
  </div>
</div> 
 </div> 
</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'

export default {
    name: 'NewCustomer',
    data(){
        return{
            customer:{
                id:0,
                document_number: '',
                first_name: '',
                last_name: '',
                address: '',
                birthday: '',
                phone_number: '',
                email: ''
            },
            
        }
   },
   methods: {
   cancel(){
      this.$router.push({name: 'Customers'})
   },
   
   async saveCustomer(){
        
        const res = await axios.post(`http://127.0.0.1:8000/api/customers/`, this.customer)
        console.log(res);
        if (res.status == 200){
           this.$router.push({name: 'Customers'})
           Swal.fire({
               position: 'top-end',
               icon: 'success',
               title: 'Customer has been saved',
               showConfirmButton: false,
               timer: 2000           
           })
       }
   }
}

}
</script>