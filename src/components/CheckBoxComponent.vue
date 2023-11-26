<script>
export default {
  name: "CheckBoxComponent",
  props: ['checked', 'product'],
  data() {
    return {
      myCheck: {},
    }
  },
  created() {
    this.myCheck.name = this.checked.name;
    this.myCheck.value = this.checked.value;
    this.myCheck.currency = this.checked.currency;
    this.myCheck.factor = this.checked.factor;
    this.myCheck.isSelect = this.checked.isSelect;
  },
  methods: {
    onSaveCheck() {
      const myCheckDataSave = this.myCheck.clone;
      this.$emit('saveCheck', myCheckDataSave);
    }
  },
  computed: {}
}
</script>

<template>
  <div class="checkbox__component">
    <div class="checkbox__checked" v-if="checked.isSelect">
      <input type="radio" class="current__radio" :name="product.name" :id="checked.name" value="true"
             v-model="myCheck.isSelect" checked>
      <label :for="checked.name" class="currency__label">{{ checked.currency }}</label>
    </div>
    <div class="checkbox__not__checked" v-else>
      <input type="radio" class="current__radio" :name="product.name" :id="checked.name" value="false"
             v-model="myCheck.isSelect">
      <label :for="checked.name" class="currency__label">{{ checked.currency }}</label>
    </div>
  </div>
</template>

<style scoped>

</style>