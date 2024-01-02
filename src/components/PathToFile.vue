<template>
    <div>
        <label
            >Введіть шлях <input type="text" :class="{ 'incorrect-path': isPathInCorrect }" v-model="userPath"
        /></label>
    </div>
</template>

<script>
export default {
    name: 'PathToFile',
    data() {
        return {
            isPathInCorrect: false,
        }
    },
    props: {
        modelValue: {
            type: String,
        },
        modelModifiers: {
            default: () => ({}),
        },
    },
    computed: {
        userPath: {
            get() {
                return this.modelValue
            },
            set(newPath) {
                if (this.modelModifiers.checkPath) {
                    if (newPath.endsWith('.js')) this.isPathInCorrect = false
                    else this.isPathInCorrect = true
                }
                this.$emit('update:modelValue', newPath)
            },
        },
    },
}
</script>

<style lang="scss" scoped>
.incorrect-path {
    background-color: red;
}
</style>
