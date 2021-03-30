<template>
    <div class="item">
        <div>这是标题{{props.item}}</div>
        <div>这是内容</div>
        <hr />
    </div>
</template>

<script setup>
    import { defineProps, reactive } from 'vue'

    const props = defineProps({
        item: Number
    })

    const state = reactive({ count: 0 })
</script>

<style scoped>
    a {
        color: #42b983;
    }

    .item {
        height: 50px;
    }
</style>