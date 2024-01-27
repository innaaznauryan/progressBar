<template>
    <div id="bar" :style="{backgroundImage: 'conic-gradient(yellow ' + deg + 'deg, #9384be 0deg)'}">
        <div id="inner">
            <div id="progress">{{ level * 100 }}%</div>
        </div>
    </div>
    <BaseInput v-model="level"/>
</template>

<script>
import BaseInput from "./BaseInput.vue"

export default {
    data() {
        return {
            level: 0
        }
    },
    computed: {
        deg() {
            return this.level * 360
        }
    },
    components: {
        BaseInput
    }
}
</script>

<style scopped>
#bar {
    height: 200px;
    width: 200px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
}

#inner {
    background-color: purple;
    border-radius: 50%;
    width: 90%;
    height: 90%;
    display: flex;
    justify-content: center;
    align-items: center;
}

#progress {
    color: yellow;
    font-size: 32px;
}
</style>