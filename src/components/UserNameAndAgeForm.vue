<template>
    <div>
        <label>Введіть імя <input type="text" v-model="nameValue" :class="{ 'empty-name': isNameEmpty }" /></label>
        <label>Введітть ваш вік <input type="number" v-model="ageValue" :class="{ [ageClass]: ageValue }" /></label>
    </div>
</template>

<script>
export default {
    name: 'UserNameAndAgeForm',
    data() {
        return {
            isNameEmpty: false,
            ageClass: null,
        }
    },
    props: {
        name: {
            type: String,
        },
        nameModifiers: {
            default: () => ({}),
        },
        age: {
            type: Number,
        },
        ageModifiers: {
            default: () => ({}),
        },
    },
    computed: {
        nameValue: {
            get() {
                return this.name
            },
            set(newNameValue) {
                if (this.nameModifiers.isNameEntered) {
                    //  if (newNameValue === '') this.isNameEmpty = !this.isNameEmpty
                    this.isNameEmpty = newNameValue === '' ? true : false
                }
                this.$emit('update:name', newNameValue)
            },
        },
        ageValue: {
            get() {
                return this.age
            },
            set(newAgeValue) {
                if (this.ageModifiers.has18Year) {
                    if (newAgeValue < 18) this.ageClass = 'age-less-18'
                    else this.ageClass = 'age-more-18'
                }
                if (newAgeValue === '') {
                    newAgeValue = null
                }
                this.$emit('update:age', newAgeValue)
            },
        },
    },
}
</script>

<style lang="scss" scoped>
.empty-name {
    background-color: red;
}
.age-less-18 {
    background-color: red;
}
.age-more-18 {
    background-color: green;
}
</style>
