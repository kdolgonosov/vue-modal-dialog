<template>
    <div class="modal" @click="$emit('close')">
        <div class="modal-container" @click="(e) => e.stopPropagation()">
            <h2 class="title">{{ title }}</h2>
            <form class="modal-form">
                <template v-for="(field, i) in fields">
                    <div class="input-wrapper" :class="{ 'input-wrapper-small': twoColumns }">
                        <label>{{ field.label }}</label>
                        <select
                            v-if="field.type === 'select'"
                            v-model.number="formData[field.name]"
                            class="input"
                        >
                            <option value="none" selected disabled hidden>Select an Option</option>
                            <option v-for="option in field.options" :value="option.value">
                                {{ option.placeholder }}
                            </option>
                        </select>
                        <input
                            v-else-if="field.type === 'text'"
                            type="text"
                            v-model="formData[field.name]"
                            class="input"
                        />
                        <input
                            v-else
                            type="number"
                            v-model.number="formData[field.name]"
                            class="input"
                        />
                    </div>
                </template>
                <div class="button-wrapper">
                    <button class="button" @click="$emit('close')">Отмена</button>
                    <input class="button" type="submit" @click="handleSubmit" />
                </div>
            </form>
        </div>
    </div>
</template>

<script setup>
import { defineProps, computed, reactive, toRaw } from 'vue';

const props = defineProps({
    url: {
        type: String,
    },
    twoColumns: {
        type: Boolean,
    },
    selectedFields: {
        type: Array,
    },
    title: {
        type: String,
    },
});
const formData = reactive({});
const availableFields = reactive([
    {
        name: 'manager',
        label: 'Менеджер',
        type: 'select',
        options: [
            { value: 1, placeholder: 'Менеджер №1' },
            { value: 2, placeholder: 'Менеджер №2' },
            { value: 3, placeholder: 'Менеджер №3' },
        ],
    },
    {
        name: 'productName',
        label: 'Название продукта',
        type: 'text',
    },
    {
        name: 'jiraLink',
        label: 'Ссылка в jira',
        type: 'text',
    },
    {
        name: 'domain',
        label: 'Домен',
        type: 'select',
        options: [
            { value: 1, placeholder: 'Бэк-офис' },
            { value: 2, placeholder: 'Техплатформа' },
            { value: 3, placeholder: 'Офис больших данных' },
            { value: 3, placeholder: 'Цифровой опыт поставщика' },
        ],
    },
    {
        name: 'employee',
        label: 'Сотрудник',
        type: 'select',
        options: [
            { value: 1, placeholder: 'Сотрудник №1' },
            { value: 2, placeholder: 'Сотрудник №2' },
            { value: 3, placeholder: 'Сотрудник №3' },
            { value: 3, placeholder: 'Сотрудник №4' },
        ],
    },
    {
        name: 'supervisor',
        label: 'Руководитель сотрудника',
        type: 'select',
        options: [
            { value: 1, placeholder: 'Руководитель №1' },
            { value: 2, placeholder: 'Руководитель №2' },
            { value: 3, placeholder: 'Руководитель №3' },
            { value: 3, placeholder: 'Руководитель №4' },
        ],
    },
    {
        name: 'capitalType',
        label: 'Тип ставки',
        type: 'select',
        options: [
            { value: 1, placeholder: 'OPEX' },
            { value: 2, placeholder: 'CAPEX' },
        ],
    },
    {
        name: 'unit',
        label: 'Бизнес-единица',
        type: 'select',
        options: [
            { value: 1, placeholder: 'MVM' },
            { value: 2, placeholder: 'MTech' },
        ],
    },
    {
        name: 'capitalization',
        label: 'Процент капитализации',
        type: 'number',
    },
    {
        name: 'rank',
        label: 'Должность',
        type: 'text',
    },
]);
const fields = computed(() => {
    return availableFields.filter((item) => props.selectedFields.includes(item.name));
});
const handleSubmit = (e) => {
    e.preventDefault();
    // fetch('https://jsonplaceholder.typicode.com/posts', {
    //     method: 'POST',
    //     body: JSON.stringify(formData),
    //     headers: {
    //         'Content-type': 'application/json; charset=UTF-8',
    //     },
    // })
    //     .then((response) => response.json())
    //     .then((json) => console.log(json));
    console.log('Sent POST to: ', url.value);
    console.log('Data: ', toRaw(formData));
};
</script>

<style scoped>
.title {
    margin: 0 0 16px 0;
}
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.4);
    overflow: hidden;
    overflow-y: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
}
.modal-container {
    background-color: #fff;
    border-radius: 25px;
    width: 500px;
    padding: 50px;
}
.modal-form {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: wrap;
}
.input-wrapper {
    margin-bottom: 10px;
    display: flex;
    flex-direction: column;
    width: 400px;
}
.input-wrapper:last-of-type {
    margin-bottom: 0;
}
.input {
    height: 30px;
}
.input:hover {
    cursor: pointer;
}
.input-wrapper-small {
    width: 180px;
}
.modal__form_submit-btn {
    height: 35px;
}

.button-wrapper {
    width: 100%;
    margin-top: 20px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}
.button {
    width: 150px;
    height: 35px;
}
.button:hover {
    cursor: pointer;
}
</style>
