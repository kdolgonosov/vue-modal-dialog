<template>
    <ModalDialog
        v-if="isModalOpened"
        :title="title"
        :selected-fields="selectedFields"
        :url="url"
        :two-columns="twoColumns"
        @close="handleOpenModal"
    />
    <div class="container">
        <div class="button-wrapper">
            <button
                class="button"
                @click="
                    () => {
                        title = 'Форма №1';
                        selectedFields = ['manager', 'productName', 'jiraLink', 'domain'];
                        url = 'https://some.endpoint/1';
                        handleOpenModal();
                    }
                "
            >
                Пресет из ТЗ №1
            </button>
            <button
                class="button"
                @click="
                    () => {
                        title = 'Форма №2';
                        selectedFields = [
                            'employee',
                            'supervisor',
                            'capitalType',
                            'unit',
                            'capitalization',
                            'rank',
                        ];
                        url = 'https://some.endpoint/2';
                        handleOpenModal();
                    }
                "
            >
                Пресет из ТЗ №2
            </button>
            <button
                class="button"
                @click="
                    () => {
                        title = 'Кастомная форма';
                        handleOpenModal();
                    }
                "
            >
                Кастомная форма
            </button>
        </div>
        <div class="fields-selector">
            <span class="fields-selector-title">Доступные поля</span>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="manager"
                    value="manager"
                    v-model="selectedFields"
                />
                <label class="label" for="manager">Менеджер</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="productName"
                    value="productName"
                    v-model="selectedFields"
                />
                <label class="label" for="john">Название продукта</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="jiraLink"
                    value="jiraLink"
                    v-model="selectedFields"
                />
                <label class="label" for="jiraLink">Ссылка в jira</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="domain"
                    value="domain"
                    v-model="selectedFields"
                />
                <label class="label" for="domain">Домен</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="employee"
                    value="employee"
                    v-model="selectedFields"
                />
                <label class="label" for="employee">Сотрудник</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="supervisor"
                    value="supervisor"
                    v-model="selectedFields"
                />
                <label class="label" for="supervisor">Руководитель сотрудника</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="capitalType"
                    value="capitalType"
                    v-model="selectedFields"
                />
                <label class="label" for="capitalType">Тип ставки</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="unit"
                    value="unit"
                    v-model="selectedFields"
                />
                <label class="label" for="unit">Бизнес-единица</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="capitalization"
                    value="capitalization"
                    v-model="selectedFields"
                />
                <label class="label" for="capitalization">Процент капитализации</label>
            </div>
            <div class="input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="rank"
                    value="rank"
                    v-model="selectedFields"
                />
                <label class="label" for="rank">Должность</label>
            </div>
            <span class="fields-selector-title">Url для отправки запроса</span>
            <div class="url-input-wrapper">
                <input class="input" type="text" id="url" value="url" v-model="url" />
            </div>
            <div class="twocols-input-wrapper">
                <input
                    class="checkbox"
                    type="checkbox"
                    id="twoColumns"
                    value="twoColumns"
                    v-model="twoColumns"
                />
                <label class="label" for="twoColumns">Две колонки?</label>
            </div>
        </div>
        <span class="hint">Тело запроса и url выводятся в консоль.</span>
    </div>
</template>
<script setup>
import { ref } from 'vue';
import ModalDialog from './components/ModalDialog.vue';

const isModalOpened = ref(false);
const title = ref('');
const selectedFields = ref([]);
const url = ref('');
const twoColumns = ref(false);
const handleOpenModal = () => {
    isModalOpened.value = !isModalOpened.value;
};
</script>
<style scoped>
.button {
    width: 150px;
    height: 35px;
    margin-right: 15px;
}
.button:last-of-type {
    margin-right: 0;
}
.button:hover {
    cursor: pointer;
}
.container {
    display: flex;
    flex-direction: column;
}

.input-wrapper {
    display: flex;
    flex-direction: row;
    font-size: 18px;
    margin-bottom: 10px;
}
.url-input-wrapper {
    display: flex;
    flex-direction: column;
    font-size: 18px;
}
.twocols-input-wrapper {
    margin-top: 16px;
    font-size: 18px;
}
.checkbox {
    margin-right: 5px;
    width: 15px;
    height: 15px;
}
.checkbox:hover {
    cursor: pointer;
}
.label {
    line-height: 15px;
}
.button-wrapper {
    display: flex;
    flex-direction: row;
}
.fields-selector {
    display: flex;
    flex-direction: column;
}
.fields-selector-title {
    font-size: 24px;
    font-weight: 500;
}
.hint {
    max-width: 700px;
    font-size: 28px;
    font-weight: 600;
    margin-top: 20px;
}
.hint:last-of-type {
    margin-top: 5px;
}
</style>
