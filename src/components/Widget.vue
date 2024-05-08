<template>
        <main>
            <article class="card">
                <div class="buttons">
                    <TaskButtonList />
                </div>
                <div class="wrapper">
                    <div class="content">
                        <ActiveWindow />
                    </div>
                </div>
            </article>
        </main>
</template>

<script setup lang="ts">
import TaskButtonList from './TaskButtonList.vue';
import ActiveWindow from './ActiveWindow.vue';
</script>