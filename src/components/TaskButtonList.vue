<template>
    <ul>
        <li v-for="item in store.items" :key="item.id" @click="store.setSelectedItem(item)"
            :class="['task', { 'active': store.selectedItem === item }]">
            <div class="box">
                <Checkbox :checked="item.isChecked" @change="(checked: boolean) => handleCheckboxChange(item, checked)" />
                {{ item.title }}
            </div>
            <img src="../assets/edit.svg" alt="edit task" class="edit_icons" @click="store.setSelectedItem(item)" />
        </li>
    </ul>
</template>

<script setup lang="ts">
import { useStore } from '../stores/stores';
import { Item } from '../stores/stores';
import Checkbox from './ui/Checkbox.vue';

const store = useStore();

const handleCheckboxChange = (item: Item, _checked: boolean) => {
    store.toggleItem(item);

    store.items.forEach((storedItem: Item) => {
        if (item.subTasks.includes(storedItem.title)) {
            store.toggleItem(storedItem);
        }
    });
};
</script>