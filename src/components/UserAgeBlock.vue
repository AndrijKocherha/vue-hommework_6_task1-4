<template>
    <div>
        <label>Введіть ваш вік: <input type="number" v-model="yearValue" :class="colorClass" /></label>
    </div>
</template>

<script>
export default {
    name: 'UserYearBlock',
    data() {
        return {
            colorClass: null,
        }
    },
    props: {
        modelValue: {
            type: Number,
        },
        modelModifiers: {
            default: () => ({}),
        },
    },
    computed: {
        yearValue: {
            get() {
                return this.modelValue
            },
            set(yearVal) {
                if (this.modelModifiers.check) {
                    if (yearVal > 150) {
                        yearVal = null
                    }
                }
                if (this.modelModifiers.setColor && yearVal) {
                    console.log(111111)
                    if (yearVal < 10) {
                        this.colorClass = 'kid'
                    } else if (yearVal < 21) {
                        this.colorClass = 'teenager'
                    } else {
                        this.colorClass = 'adult'
                    }
                }
                //цю перевірку роблю для того щоб не було  помилки (Expected Number with value 0, got String with value "")
                if (yearVal === '') {
                    yearVal = null
                    this.colorClass = null
                }
                this.$emit('update:modelValue', yearVal)
            },
        },
    },
}
</script>

<style lang="scss" scoped>
.teenager {
    background-color: yellow;
}
.kid {
    background-color: green;
}
.adult {
    background-color: orange;
}
</style>
