<script>
import CheckBoxComponent from "@/components/CheckBoxComponent.vue";

export default {
  name: "ProductDetails",
  components: {
    CheckBoxComponent
  },
  props: ['product'],
  data() {
    return {
      showDetails: false,
      currencyList: [{name: 'dollar', value: 'USD', currency: '$', factor: 1.0, isSelect: false},
        {name: 'Euro', value: 'EURO', currency: '€', factor: 0.916369, isSelect: true},
        {name: 'Рубли', value: 'RUB', currency: '₽', factor: 88.81, isSelect: false}],
      myProduct: '',
    }
  },
  computed: {
    getStringCurrentValue() {
      let  text;
      this.currencyList.forEach((value, index, array) => {
        if (array[index].isSelect) {
          text = this.product.price * array[index].factor + ' ' + array[index].currency;
        }
      });
      return text;
    }
  },
  methods: {
    addNewCheck(data) {
      this.myProduct.isSelect = data.isSelect;
    }
  }
}
</script>

<template>
  <div class="ProductDetails">
    <p class="product__name">name: {{ product.name }}</p>
    <p class="product__price">price: {{ getStringCurrentValue }}</p>
    <div class="container__radioInput">
      <CheckBoxComponent v-for="(item,index) in currencyList" :key="index" :checked="item"
                         :product="product"></CheckBoxComponent>
    </div>
    <p class="product__quantity">quantity: {{ product.quantity }}</p>
    <button class="product__details" @click="showDetails = !showDetails">More...</button>
    <p class="product__id" v-if="showDetails">id: {{ product.id }}</p>
    <p class="product__available" v-show="showDetails">available: {{ product.available }}</p>
    <p class="product__lines">==========================================================</p>
  </div>
</template>

<style scoped>
.container__radioInput {
  display: flex;
  justify-content: center;
  flex-direction: row;
  gap: 1em;
}
.product__details {
  background-color: bisque;
  //border: none;
  box-shadow: 14px 5px 10px 2px rgba(34, 60, 80, 0.2);
}
</style>