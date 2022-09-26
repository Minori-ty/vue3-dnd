<template>
    <button @click="add">add data</button>
    <Table :list="arr"></Table>
</template>

<script setup lang="ts">
import Table from './components/Table.vue'
import { ref } from 'vue'

const arr = ref<number[]>([])

let number = 1
function add() {
    arr.value.push(number)
    number++
}
</script>

<style scoped></style>
