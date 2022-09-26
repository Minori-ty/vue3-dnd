<template>
    <Container orientation="vertical" @drop="onDrop">
        <Draggable v-for="(item, i) in props.list" :key="item">
            {{ item }}
        </Draggable>
    </Container>
</template>

<script setup lang="ts">
import { Container, Draggable } from 'vue3-smooth-dnd'
import { ref } from 'vue'
const props = defineProps<{
    list: number[]
}>()

const arr = ref<number[]>([])

function onDrop(dropResult) {
    arr.value = applyDrag(props.list, dropResult)
}

function applyDrag(arr: number[], dragResult) {
    const { removedIndex, addedIndex, payload } = dragResult

    if (removedIndex === null && addedIndex === null) return arr
    const result = [...arr]
    let itemToAdd = payload

    if (removedIndex !== null) {
        itemToAdd = result.splice(removedIndex, 1)[0]
    }
    if (addedIndex !== null) {
        result.splice(addedIndex, 0, itemToAdd)
    }
    return result
}
</script>

<style scoped></style>
