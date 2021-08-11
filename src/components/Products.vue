<template>
<div v-if="ProductList.length > 0">
    <h3 class="text-center">Lista Dodanych Produktów</h3>
    <hr>
    <div class="row product-container">
    <app-product v-for="product in ProductList">
        <img class="card-img-top" :src="product.selectedImage" :alt="product.title">
        <div class="card-body">
          <h5 class="card-title"><small>{{product.title}}</small></h5>
          <small>
            <strong>Sztuka : </strong>{{product.count}}
          </small>
          <br>
          <small>
            <strong>Cena : </strong>{{product.price}}
          </small>
          <br>
          <small>
            <strong>Całkowity : </strong>{{product.totalPrice}}
          </small>
        </div>
    </app-product>
    </div>  
</div>
</template>


<script>
import { eventBus } from '../main';
import Product from './Product';
export default {
    components : {
        appProduct : Product
    },
    data(){
        return {
            ProductList: [],
        }
    },
    created(){
        eventBus.$on("ProductAdded", (product) => {
            if(this.ProductList.length < 10){
                this.ProductList.push(product);
                eventBus.$emit("progressBar", this.ProductList.length);
            } else {
                alert("nie możesz dodać więcej produktów");
            }
        })
    }
}
</script>