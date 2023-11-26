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
      newQuantity: '',
      newAvailable: '',
    }
  },
  created() {
    this.newAvailable = this.product.available;
    this.newQuantity = this.product.quantity;
  },
  computed: {
    getStringCurrentValue() {
      let text;
      this.currencyList.forEach((value, index, array) => {
        if (array[index].isSelect) {
          text = array[index].currency + ' ' + this.product.price * array[index].factor;
        }
      });
      return text;
    },
    isAvailable() {
      if (this.newAvailable) {
        return 'available';
      } else {
        return 'Out of stock';
      }
    },

  },
  methods: {
    toggle() {
      this.showDetails = !this.showDetails;
    },
    updateCheck(data) {
      this.currencyList.forEach(el => {
        el.isSelect = el === data.checkBox;
      });
    },
    increase() {
      this.newQuantity += 1;
      if (this.newQuantity > 0) {
        this.newAvailable = true;
      }
      this.onSaveQuantity();
    },
    decrease() {
      if (this.newAvailable) {
        this.newQuantity -= 1;
        if (this.newQuantity <= 0) {
          this.newAvailable = false;
        }
        this.onSaveQuantity();
      }
    },
    onSaveQuantity() {
      const dataUpdate = {
        searchProduct: this.product,
        newQuantity: this.newQuantity,
        newAvailable: this.newAvailable,
      }
      this.$emit('dataQuantityUpdate', dataUpdate)

    },
  }
}
</script>

<template>
  <div class="ProductDetails">
    <p class="product__name">name: {{ product.name }}</p>
    <p class="product__price">price: {{ getStringCurrentValue }}</p>
    <div class="container__radioInput">
      <CheckBoxComponent v-for="(item,index) in currencyList" :key="index" :checked="item"
                         :product="product" @saveCheck="updateCheck"></CheckBoxComponent>
    </div>
    <p class="product__quantity">quantity: {{ product.quantity }}</p>
    <button class="product__increase" @click="increase">+1</button>
    <button class="product__decrease" @click="decrease">-1</button>
    <button class="product__details" @click="toggle">More...</button>
    <p class="product__id" v-if="showDetails">id: {{ product.id }}</p>
    <p class="product__available" v-show="showDetails">available: {{ isAvailable }}</p>
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
  box-shadow: 14px 5px 10px 2px rgba(34, 60, 80, 0.2);
}

.product__decrease, .product__increase {
  background-color: bisque;
  box-shadow: 14px 5px 10px 2px rgba(34, 60, 80, 0.2);
}
</style>