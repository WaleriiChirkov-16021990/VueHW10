<script>
export default {
  name: "CheckBoxComponent",
  props: ['checked', 'product'],
  data() {
    return {
      myCheck: true,
    }
  },
  created() {
    this.myCheck = this.checked.isSelect;
  },
  methods: {
    onSaveCheck() {
      const updateCheck = {
        checkBox: this.checked,
        updateIsSelect: this.myCheck,
      }
      this.$emit('saveCheck', updateCheck);
    },

  },
  computed: {}
}
</script>

<template>
  <div class="checkbox__component">
    <div class="checkbox__checked" v-if="checked.isSelect">
      <input type="radio" class="current__radio" :name="product.name" :id="checked.name"
             v-model="myCheck" :value="checked.isSelect" checked>
      <label :for="checked.name" class="currency__label">{{ checked.currency }}</label>
    </div>
    <div class="checkbox__not__checked" v-else>
      <input type="radio" class="current__radio" :name="product.name" :id="checked.name"
             v-model="myCheck" :value="!checked.isSelect" @click="onSaveCheck">
      <label :for="checked.name" class="currency__label">{{ checked.currency }}</label>
    </div>
  </div>
</template>

<style scoped>

</style>