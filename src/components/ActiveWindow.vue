<template>
    <div v-if="store.selectedItem" class="activeBlock">
        <div>
            <div>
                <input type="text" class="activeBlock-title" v-model="newTitle" @change="handleTitleChange" />
                <p class="activeBlock-text">{{ store.selectedItem.text }}</p>
            </div>
            <ul>
                <li v-for="item in store.items" :key="item.id">
                    <Checkbox :checked="subTasksState[item.title] || false"
                        @change="(checked: boolean) => handleCheckboxChange(item, checked)" />
                    {{ item.title }}
                </li>
            </ul>
        </div>
        <Button @click="handleSave" buttonTxt="Сохранить" />
        <div v-if="saveSuccess" class="saveSuccess">
            Изменения успешно сохранены!
        </div>
    </div>
    <div v-else class="text">Выберите элемент для просмотра деталей</div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { useStore } from '../stores/stores';
import { Item } from '../stores/stores';
import Button from './ui/Button.vue';
import Checkbox from './ui/Checkbox.vue';

const store = useStore();

const newTitle = ref<string>('');
const subTasksState = ref<Record<string, boolean>>({});
const saveSuccess = ref(false);

watch(() => store.selectedItem, (selectedItem) => {
    if (selectedItem) {
        newTitle.value = selectedItem.title;
        const subTasksMap: Record<string, boolean> = {};
        store.items.forEach((item: Item) => {
            subTasksMap[item.title] = selectedItem.subTasks.includes(item.title);
        });
        subTasksState.value = subTasksMap;
    }
});

const handleTitleChange = (event: Event) => {
    newTitle.value = (event.target as HTMLInputElement).value;
};

const handleSave = () => {
    if (store.selectedItem) {
        const newSubTasks: string[] = [];
        for (const subTask in subTasksState.value) {
            if (subTasksState.value[subTask]) {
                newSubTasks.push(subTask);
            }
        }
        store.selectedItem.subTasks = newSubTasks;

        store.editItemTitle(store.selectedItem, newTitle.value);
        saveSuccess.value = true;
        setTimeout(() => {
            saveSuccess.value = false;
        }, 3000);
    }
};

const handleCheckboxChange = (item: Item, checked: boolean) => {
    subTasksState.value[item.title] = checked;
};
</script>