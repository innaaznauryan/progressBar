<template>
  <div class="container">
    <div class="progress" :style="{background: `conic-gradient(#EBE424 ${degree}deg, #4F4466 0deg`}">
      <div class="inner">
        <div class="indicator">{{ percent }}%</div>
      </div>
    </div>
    <BaseInput v-model="value"/>
  </div>
</template>

<script>
import BaseInput from "./BaseInput.vue"

export default {
  data() {
    return {
      value: 0,
      percent: 0,
      degree: 0
    }
  },
  watch: {
    value() {
      this.percent = 0
      this.degree = 0
      let percentInterval = null
      let degreeInterval = null
      clearInterval(percentInterval)
      clearInterval(degreeInterval)

      if(!percentInterval) {
        percentInterval = setInterval(() => {
          if (this.percent < Math.round(this.value * 100)) {
            this.percent++
          } else {
            clearInterval(percentInterval)
            percentInterval = null
          }
        }, 10)
      }

      if(!degreeInterval) {
        degreeInterval = setInterval(() => {
          if (this.degree < this.value * 360) {
            this.degree++
          } else {
            clearInterval(degreeInterval)
            degreeInterval = null
          }
        }, 2.7)
      }
    }
  },
  components: {
    BaseInput
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
</style>