<template>
    <div class="page-category">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h2 class="is-size-2 has-text-centered">{{category.name}}</h2>
            </div>
        <div 
    class="columns is-5"
    v-for="product in category.products"
    v-bind:key="product.id">
    <div class="box">
      <figure class="image mb-4">
        <img v-bind:src="product.get_thumbnail">
      </figure>
    <h3 class="is-size-4">{{product.name}}</h3>
    <p class="is-size-6 has-text-black">₹{{product.price}}</p>
    <router-link v-bind:to="product.get_absolute_url" class="button is-dark mt-4">View Details </router-link>
    </div>
    </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
import {toast} from 'bulma-toast'
export default{
    name : 'Category',
    data(){
        return{
            category:{
                products: []
            }
        }
    },
    mounted(){
        this.getcategory()
    },
    methods:
    {
        getcategory(){
            const category_slug = this.$route.params.category_slug
            axios
            .get(`/api/v1/products/${category_slug}/`)
            .then(response => {
             this.category = response.data
             document.title = this.category.name+ ' | Apple Mobiles'
             })
            .catch(error => {
            console.log(error)
            toast(
            {
            message:'something went wrong',
            type:'is-danger',
            position:'top-right',
            pauseOnHover:true,
            duration:1000,
            dismissible:true,
             })
            })
        }

    }
}
</script>
