<template>
    <div class="task-body">
        <div class="task-body__condition">
            Задача 1. Розробити компонент для введення віку користувача (з підтримкою v-model). При заданні модифікатора
            check не допускати введення некоректного віку (вік не може бути більшим за 150). При заданні модифікатора
            setColor задавати фон (вік менше 10 – зелений, від 10 до 21 – жовтий, інакше – оранжевий).
        </div>
        <user-age-block v-model.check.setColor="userYear" />
        <div>{{ userYear }}</div>
    </div>
    <div class="task-body">
        <div class="task-body__condition">
            Задача 2. Розробити компонент (з підтримкою v-model), який дозволяє вводити шлях до файлу js (URL, що
            закінчується розширенням js). При заданні модифікатора checkPath відображати червоним фоном input, якщо шлях
            некоректний.
        </div>
        <path-to-file v-model.checkPath="userPath" />
        <div>{{ userPath }}</div>
    </div>
    <div class="task-body">
        <div class="task-body__condition">
            Задача 3. Розробити компонент (з підтримкою v-model), який дозволяє вводити e-mail з домену “edu” (приклад:
            ivan- hopko@inv.mn.edu). Частинка «@inv.mn.edu» додається автоматично (користувач не вводить її). При
            заданні модифікатора check відображати червоним фоном input, якщо некоректний.
        </div>
        <email-entering v-model.check="userMail" />
        <div>{{ userMail }}</div>
    </div>
    <div class="task-body">
        <div class="task-body__condition">
            Задача 4. Розробити компонент для вводу віку користувача та імені. Робити форматування при заданні
            відповідних модифікаторів відповідних полів input:
            <ul>
                <li>ім’я користувача - у випадку порожнього поля (червони фон)</li>
                <li>вік (вік менший за 18 – колір фону червоний, інакше – зелений).</li>
            </ul>
        </div>
        <user-name-and-age-form v-model:name.isNameEntered="userName" v-model:age.has18Year="userAgeTwo" />
        <div>name: {{ userName }}</div>
        <div>age: {{ userAgeTwo }}</div>
    </div>
</template>

<script>
import EmailEntering from './components/EmailEntering.vue'
import PathToFile from './components/PathToFile.vue'
import UserAgeBlock from './components/UserAgeBlock.vue'
import UserNameAndAgeForm from './components/UserNameAndAgeForm.vue'

export default {
    name: 'App',
    components: { UserAgeBlock, PathToFile, EmailEntering, UserNameAndAgeForm },
    data() {
        return {
            userYear: null,
            userPath: null,
            userMail: null,
            userAgeTwo: null,
            userName: null,
        }
    },
}
</script>

<style lang="scss">
@import './assets/style';
</style>
