<template>
    <div>
        <label
            >Введіть e-mail
            <input
                :key="updateKey"
                ref="mail"
                type="text"
                v-model="userMail"
                :class="{ 'incorrect-mail': isInCorrectMail }"
        /></label>
    </div>
</template>

<script>
const startEmail = '@inv.mn.edu'
export default {
    name: 'EmailEntering',
    data() {
        return {
            isInCorrectMail: false,
            updateKey: 0,
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
        userMail: {
            get() {
                return this.modelValue
            },
            set(newMail) {
                if (newMail.length === 1 && !newMail.endsWith(startEmail)) {
                    newMail = `${newMail}${startEmail}`
                    //  як я розумію це не дуже добрий варіант (хоча працює ніби)
                    //  setTimeout(() => {
                    //      this.$refs.mail.setSelectionRange(1, 1)
                    //  }, 1)
                    this.$nextTick(() => {
                        this.updateKey++
                        this.$nextTick(() => {
                            this.$refs.mail.focus()
                            this.$refs.mail.setSelectionRange(1, 1)
                        })
                    })
                }
                if (this.modelModifiers.check) {
                    console.log(11111111111)
                    this.isInCorrectMail = !newMail.endsWith(startEmail)
                }
                this.$emit('update:modelValue', newMail)
            },
        },
    },
}
</script>

<style lang="scss" scoped>
.incorrect-mail {
    background-color: red;
}
</style>
