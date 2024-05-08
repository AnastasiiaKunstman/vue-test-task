<template>
    <button v-bind="props" class="button">{{ props.buttonTxt }}</button>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';

const props = defineProps({
    buttonTxt: String
});
</script>