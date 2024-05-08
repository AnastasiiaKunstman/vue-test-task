<template>
    <input type="checkbox" :checked="props.checked" @change="props.onChange" class="ui_checkbox" />
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';

interface CustomCheckboxProps {
    checked: boolean;
    onChange: (checked: boolean) => void;
}

const props: CustomCheckboxProps = defineProps();

const isChecked = ref(props.checked);

watch(() => props.checked, (newValue: boolean) => {
    isChecked.value = newValue;
});
</script>