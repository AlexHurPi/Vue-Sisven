<template>
    <div class="container">    
        <h1 class="text-start">Categories List
        <button @click="newCategory()"  
        class="btn btn-success mx-2">
        <font-awesome-icon icon="plus" />
        </button>
    </h1>
        <table class="table">
        <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Id</th>
                <th scope="col">Name</th>
                <th scope="col">Description</th>                        
            </tr>
        </thead>
        <tbody>       
            <tr v-for="(category,index) in categories" :key="index">
                <th scope="row">{{ index + 1 }}</th>
                <td>{{ category.id }}</td>
                <td>{{ category.name }}</td>
                <td>{{ category.description }}</td>  
                <td>                    
               <button @click="deleteCategory(category.id)"
                   class="btn btn-danger mx-2">
                   <font-awesome-icon icon="trash" />
               </button> 
               <button @click="deleteCategory(category.id)"           
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
    
    export default {
    
        name: 'Category',
        data(){
            return{
               categories: []
            }
        },
        mounted() {
            axios
                .get('http://127.0.0.1:8000/api/categories')
                .then(response => (this.categories = response.data.categories))
        },
    }
    </script>