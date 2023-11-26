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
      product.available = product.quantity > 1;
    });
  },
  methods: {
    updateProduct(data) {
      this.getLeftOvers();
      this.productList.forEach(product => {
        if (product === data.searchProduct) {
          product.quantity = data.newQuantity;
          product.available = data.newAvailable;
        }
      })
    }, getLeftOvers() {
      this.productList.forEach(product => {
        product.available = product.quantity > 1;
      });
    },
  },
  computed: {}
}
</script>

<template>
  <div>
    <ProductDetails v-for="(item,index) in this.productList" :key="index" :product="item"
                    @dataQuantityUpdate="updateProduct"></ProductDetails>
  </div>
</template>

<style scoped>

</style>