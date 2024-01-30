<template>
  <div class="container">
    <div class="progress" :style="{background: `conic-gradient(#EBE424 ${degree}deg, #4F4466 0deg`}">
      <div class="inner">
        <div class="indicator">{{ percent }}%</div>
      </div>
    </div>
    <input type="number" v-model.number="value">
    <p class="error">{{ error }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: 0,
      percent: 0,
      degree: 0,
      error: null,
      percentInterval: null,
      degreeInterval: null
    }
  },
  watch: {
    value: function () {
      if (this.value < 0 || this.value > 1 || this.value === null) {
        this.error = "Please enter a number between 0 and 1"
        this.value = null
        return
      }

      this.error = null

      if (this.percentInterval) {
        clearInterval(this.percentInterval)
        this.percentInterval = null
      }
      if (this.degreeInterval) {
        clearInterval(this.degreeInterval)
        this.degreeInterval = null
      }

      this.percentInterval = setInterval(() => {
        if (this.percent === Math.round(this.value * 100)) {
          return
        } else if (this.percent < Math.round(this.value * 100)) {
          this.percent++
        } else {
          this.percent--
        }
      }, 10)

      this.degreeInterval = setInterval(() => {
        if (this.degree === Math.round(this.value * 360)) {
          return
        } else if (this.degree < Math.round(this.value * 360)) {
          this.degree++
        } else {
          this.degree--
        }
      }, 2.7)
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

.error {
  color: red;
  padding: 20px;
  font-size: 20px;
}
</style>