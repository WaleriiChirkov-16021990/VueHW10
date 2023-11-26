<script>
import ProductDetails from "@/components/ProductDetails.vue";

export default {
  name: "ProductList",
  components: {ProductDetails},
  data() {
    return {
      productList: [
        {
          id: 1, name: 'Product1',
          price: 1,
          quantity: 5,
          available: false,
        }, {
          id: 2,
          name: 'Product2',
          price: 2,
          quantity: 0,
          available: false,
        }, {
          id: 3,
          name: 'Product3',
          price: 3,
          quantity: 10,
          available: false,
        }, {
          id: 4,
          name: 'Product4',
          price: 4,
          quantity: 15,
          available: false,
        }
      ],
    }
  },
  created() {
    this.productList.forEach(product => {
      product.available = product.quantity > 0;
    })
  }
}
</script>

<template>
  <div>
    <ProductDetails v-for="(item,index) in this.productList" :key="index" :product="item"></ProductDetails>
  </div>
</template>

<style scoped>

</style>