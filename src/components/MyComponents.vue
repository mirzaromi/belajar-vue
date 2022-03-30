<template>
<div class="backdrop" @click.self="hideModal">
    <div class="modal" :class="{custom : theme === 'custom'}">
        <h1>{{ name }}</h1>
        <p>{{ text }}</p>
        <img src="../assets/img/balik pondok.png" alt="" width="50">
    </div>
</div>
</template>

<script setup>
    const props = defineProps(['name', 'text', 'theme'])
    const emit = defineEmits(['close'])
    function hideModal() {
        emit('close')
    }
</script>

<style>
    .backdrop{
        width: 100%;
        background-color: aliceblue;
    }
    .modal.custom {
        background-color: rgb(43, 43, 199);
    }
    .modal{
        width: 500px;
        color: #222;        
        background-color: aquamarine;
    }
</style>