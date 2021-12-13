<template>
  <div class="container">
    <div class="card mt-4">
      <div class="card-header">
        Products car
      </div>
      <div class="card-body">
        <template v-if="products.length === 0">
          <p>No existen productos</p>
        </template>
        <template v-if="products.length > 0">
          <input type="email" v-model="email" class="form-control  " placeholder="Email">
          <table class="table table-hover table-borderless">
            
            <thead>
              <tr>
                <th scope="col"></th>
                <th scope="col">Name</th>
                <th scope="col">Price</th>
                <th scope="col">Inventory</th>
                <th scope="col">Quantity</th>
                <th scope="col"></th>
              </tr>
            </thead>
            <tbody>
              <template v-for="product in products" :key="product.id">
                  <ProductCar :product="product" :reloadCarFun="reloadCarFun" />
              </template>
            </tbody>
          </table>
          <button @click="buyNow" class="btn btn-warning btn-fill">Buy now</button>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import { get, removeAll } from '../services/car';
import { createOrder } from '../services/order'
import { ref, watchEffect } from 'vue';
import ProductCar from '../components/ProductCar.vue';
import Swal from 'sweetalert2';
import { getProducts } from '../services/product';

export default {
  components: {
    ProductCar
  },
  setup() {
    const products = ref([]);
    const reloadCar = ref(false);
    const email=ref('');
    

    watchEffect(() => {
      
      reloadCar.value;

      products.value = get();

    });

    const reloadCarFun = () => {
      reloadCar.value = !reloadCar.value;
    }

    const buyNow = async () => {
      //console.log(products.value);
      //console.log(email.value);
     
     if (email.value===''){
              Swal.fire({
        position:"top-end",
        icon:'error',
        title:'Email requerido',
        showConfirmButton:false,
        timer:2000,
              }); 
         return;
       
      
      }
      for (const product of products.value){
        if (product.quantity===0){
        Swal.fire({
        position:"top-end",
        icon:'error',
        title:'Cantidad Requerida',
        showConfirmButton:false,
        timer:2000,
              }); 
         return;
       
      
      }
      }
      for (const product of products.value){
        if (product.quantity===0){
        Swal.fire({
        position:"top-end",
        icon:'error',
        title:'Cantidad Requerida',
        showConfirmButton:false,
        timer:2000,
              }); 
         return;
       
      
      }
      }
      for (const product of products.value){
        if (product.quantity===0){
        Swal.fire({
        position:"top-end",
        icon:'error',
        title:'Cantidad Requerida',
        showConfirmButton:false,
        timer:2000,
              }); 
         return;
       
      
      }
      }
      for (const product of products.value){
        if (product.inventory===0){
        Swal.fire({
        position:"top-end",
        icon:'error',
        title:'Agotado',
        showConfirmButton:false,
        timer:2000,
              }); 
         return;
       
      
      }
      }
  
  
  
      

      Swal.fire({
      allowOutsideClick: false,
      text: 'Loading...'
      });
      
      Swal.showLoading();
      const order ={
      email:email.value,
      product:products.value,
      }
       
       Swal.showLoading();
       console.log(order);
      const resp=  await createOrder(order);
      
      
    
     
     if(!resp.ok){
        console.log("Error al guardar");

      }else { 
        console.log("ok");
        removeAll();

        


        products.value=[];
        
        email.value='';
    


        
      }


      Swal.close();
      

    
    
    }

    return {
      products,
      reloadCarFun,
      buyNow,
      email,
      
      
      
     
    }

  }
}
</script>

<style scoped>
  .card-header {
    background: #de1822;
    color: white;
    font-size: 16px;
  }
</style>