<template>
    <div class="container"> 
    <h1 class="text-start">Paymode List |
        <button @click="newPaymode()"  
        class="btn btn-success mx-2">
        <font-awesome-icon icon="plus" />
        </button>
    </h1>
<table class="table">
    <thead>
        <tr>
            <th scope="col">Id</th>
            <th scope="col">Name</th>
            <th scope="col">Observation</th> 
            <th scope="col">Actions</th>             
        </tr>
    </thead>
    <tbody>       
        <tr v-for="(paymode, index) in paymodes" :key="index">
            <th scope="row">{{ index + 1 }}</th>
            <td>{{ paymode.id }}</td>
            <td>{{ paymode.name }}</td>
            <td>{{ paymode.observation }}</td>
            <td>
                <button @click="deletePaymode(paymode.id)"
                    class="btn btn-danger mx-2">
                    <font-awesome-icon icon="trash" />
                </button> 
                <button @click="editPaymode(paymode.id)"           
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

    name: 'Paymode',
    data(){
        return{
            paymodes: []
        }
   },
   methods: {
       deletePaymode(id){
           Swal.fire({
              title: `Do you want to delete the Paymode with id ${id}?`,
              showCancelButton: true,
              confirmButtonText: 'Delete',
              }).then((result) => {
              /* Read more about isConfirmed, isDenied below */
              if (result.isConfirmed) {
                 //Swal.fire('Saved!', '', 'success')
                 axios.delete(`http://127.0.0.1:8000/api/paymodes/${id}`)
                 .then(response => {
                     if (response.data.success){
                        Swal.fire('Deleted!! ', '', 'success')
                        this.paymodes = response.data.paymodes
                     }
                 })
               }
           })
    },
    editPaymode(id){
    this.$router.push({name: 'EditarPaymode', params: { id: `${id}` }} )
},
newPaymode(){
    this.$router.push({name: 'NewPaymode'});
}
},
mounted() {
    axios
        .get('http://127.0.0.1:8000/api/paymodes')
        .then(response => (this.categories = response.data.paymodes.data))
},
}
