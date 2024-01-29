<template>
  <input type="text" :value="modelValue" @input="handleInput">
  <p class="error">{{ error }}</p>
</template>

<script>
export default {
  props: ["modelValue"],
  data() {
    return {
      error: ""
    }
  },
  methods: {
    handleInput(e) {
      if (!Number.isFinite(+e.target.value) ||
          e.target.value < 0 ||
          e.target.value > 1 ||
          e.target.value.length > 4) {
        this.error = "Please enter a number from 0 to 1 with no more than 2 digits after the decimal point"
      } else {
        this.$emit('update:modelValue', e.target.value)
        this.error = ""
      }
    }
  }
}
</script>

<style scoped>
input {
  padding: 5px;
  border: 1px solid;
  outline: 0;
  border-radius: 5px;
  font-size: 18px;
  text-align: center;
  width: 100px;
  color: #231540;
}

.error {
  color: red;
  padding: 20px;
  font-size: 20px;
}
</style>