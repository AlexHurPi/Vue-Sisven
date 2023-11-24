<template>
    <div class="container text-start">
       <h1 class="text-primary fw-bold"> Edit</h1>
       <div class="card">
           <div class="card-header fw-bold">Category</div>
      <div class="card-body">
          <form @submit.prevent="updateCategory">
        
              <div class="row mb-3">
                
                <label for="id" class="form-label">Id</label>
                
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="tag" /></div>
                    <input type="text" class="form-control" id="id" 
                    placeholder="Id Category" disabled v-model='category.id'>
                </div>
             </div>
 
            <div class="row mb-3">                
                <label for="Name" class="form-label">Name : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="namec" placeholder="Category Id" 
                       v-model='category.namec'>
                </div>
             </div>

             <div class="row mb-3">                
                <label for="Description" class="form-label">Description : </label>
                <div class="input-group">
                    <div class="input-group-text"> <font-awesome-icon icon="building" />
                    </div>
                    <input type="text" class="form-control" id="description"
                     placeholder="Category Description" v-model='category.decription'>
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
    name: 'EditarCategory',
    data(){
        return{
            category:{
                id:0,
                namec: '',
                description: ''
            },
            
        }
   },
   methods: {
   cancelar(){
      this.$router.push({name: 'Categories'})
   },
   
   async updateCategory(){
       const res = await axios.put(`http://127.0.0.1:8000/api/categories/${this.category.id}`, this.category)

       if (res.status == 200){
           this.$router.push({name: 'Categories'})
           Swal.fire({
               position: 'top-end',
               icon: 'success',
               title: 'Category has been updated',
               showConfirmButton: false,
               timer: 2000           
           })
       }
   }
},

mounted() {
    this.category.id = this.$route.params.id;
    axios.get(`http://127.0.0.1:8000/api/categories/${this.category.id}`)
        .then(response => {
            this.category = response.data.category;            
         })
    },
}
</script>