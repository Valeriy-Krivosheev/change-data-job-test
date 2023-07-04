<template>
  <div v-if="isVisible">
    <div class="popup__bg" @click.stop="hidePopup"></div>
    <form class="popup" @submit.prevent="changeInfo">
      <label>
        <div class="label__text">
          {{ info.name }}
        </div>
      </label>
      <label>
        <input type="text" v-model.trim="value" placeholder="Set new value">
      </label>

      <button class="butt-change" type="submit">Change</button>
    </form>
  </div>
</template>

<script>

export default {
  data() {
    return {
      value: '',
    }
  },
  props: {
    isVisible: Boolean,
    info: Object
  },
  methods: {
    hidePopup() {
      this.$emit('update:isVisible', false)
    },
    changeInfo() {
      if (this.value.length > 0) {
        this.$emit('newValue', { value: this.value, name: this.info.name }),
        this.hidePopup()
        this.value = ''
      }
      else {
       alert('At least 1 symbol')
      }
    }
  }
}
</script>

<style >
span {
  color: red;
  display: inline-block;
  font-size: 14px;
  margin: 5px 0;
}

.butt-change {
  border: transparent;
  background-color: #998431;
  cursor: pointer;
  padding: 15px;
  border-radius: 10px;
}

.popup__bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  z-index: 10;

}

.popup {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #fff;
  width: 400px;
  padding: 25px;
  transition: 0.5s all;
}

form {
  border-radius: 15px;
  text-align: left;
  border: 4px solid #998431;
  z-index: 11;
}

.popup label {
  width: 100%;
  margin-bottom: 25px;
  display: flex;
  flex-direction: column-reverse;
}

.popup .label__text {
  font-size: 16px;
  color: black;
  margin-bottom: 5px;
}

.popup input {
  height: 45px;
  font-size: 18px;
  border: none;
  outline: none;
  border-bottom: 1px solid #cfd0d3;
}
</style>