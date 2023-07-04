<template>
  <li class="card-item">
    <p> Hello, my name is <b> {{ card.name }}</b></p>
    <p>And my value is <b>{{ card.value }}</b> </p>
    <button @click="showPopup">
      <img src="@/assets/change.svg" alt="Change value">
    </button>
  </li>
</template>

<script>
export default {
  props: {
    card: {
      type: Object,
      default: {}
    }
  },
  methods:{
    showPopup(){
      this.$emit('showPopup', this.card.name)
      window.scrollTo(0, 0);
    }
  }
}
</script>

<style scoped>
.card-item {
  padding: 10px;
  border: 3px solid #998431;
  border-radius: 15px;
  margin-bottom: 10px;
  text-align: center;
  position: relative;
}
p{
  margin: 15px 0;
}
button{
  position: absolute;
  top: 2px;
  right: 2px;
  background-color: transparent;
  cursor: pointer;
  border-color: transparent;
}
</style>