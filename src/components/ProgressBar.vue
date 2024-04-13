<template>
  <div class="container">
    <div class="progress" :style="{ background: `conic-gradient(#EBE424 ${degree}deg, #4F4466 0deg` }">
      <div class="inner">
        <div class="indicator">{{ percent }}%</div>
      </div>
    </div>
    <input type="number" v-model.number="input">
    <p class="error"><span>{{ error }}</span></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: 0,
      percent: 0,
      degree: 0,
      error: null,
    }
  },
  watch: {
    input: function () {
      if (this.input < 0 || this.input > 1 || this.input === null) {
        this.error = "Please enter a number between 0 and 1"
        this.input = null
        return
      }
      this.error = null

      const zero = document.timeline.currentTime

      const animate = (timeStamp) => {
        const elapsed = (timeStamp - zero) / 1000
        if (elapsed < 1) {
          this.percent = Math.round(elapsed * this.input * 100)
          this.degree = Math.round(elapsed * this.input * 360)
          requestAnimationFrame(animate)
        } else {
          this.percent = Math.round(this.input * 100)
          this.degree = Math.round(this.input * 360)
        }
      }

      requestAnimationFrame(animate)
    }
  }
}
</script>

<style>
.container {
  text-align: center;
}

.progress {
  height: 200px;
  width: 200px;
  margin: 20px auto;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.inner {
  background-color: #231540;
  border-radius: 50%;
  width: 85%;
  height: 85%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.indicator {
  color: #EBE424;
  font-size: 32px;
}

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

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
}

input[type="number"] {
  -moz-appearance: textfield;
}

.error {
  color: red;
  padding: 20px;
  font-size: 18px;
  height: 32px;
}
</style>