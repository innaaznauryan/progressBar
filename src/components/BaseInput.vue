<template>
    <input type="text" :value="modelValue" @input="handleInput">
</template>

<script>
export default {
    props: ["modelValue"],
    methods: {
        handleInput(e) {
            if(!Number.isFinite(+e.target.value) || 
            e.target.value < 0 || 
            e.target.value > 1 || 
            e.target.value.length > 4) {
                return
            }
            this.$emit('update:modelValue', e.target.value)
        }
    }
}

</script>