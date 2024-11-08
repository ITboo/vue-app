<script setup>
import { ref, computed } from "vue"

const _item_text = ref("")
const _item_list = ref([])
const _pending = computed(() => {
    return _item_list.value.filter(item => !item.checked)
})
const _done = computed(() => {
    return _item_list.value.filter(item => item.checked)
})

function clearitem() {
    _item_text.value = ""
}

function additem() {
    if (_item_text.value != "") {
        _item_list.value.push({ id: _item_list.value.length + 1, text: _item_text.value, checked: false })
        clearitem()
    }
}

</script>

<template>
    <div class="item-container">

        <div class="">
            <h1>
                List
            </h1>
        </div>

        <div class="">
            <input class="" type="text" autofocus v-model="_item_text" @keyup.enter="additem()"
                placeholder="Type here your to-do item...">
            <button class="" @click="clearitem()">
                Clear
            </button>
            <button class="" @click="additem()">
                Add
            </button>
        </div>

        <div class="">Pending ({{ _pending.length }})</div>
        <div class="" v-for="item in _pending" :key="item.id">
            <label>
                <input type="checkbox" v-model="item.checked">
                <span class="">
                    {{ item.text }}
                </span>
            </label>
        </div>
        <div class="" v-show="_pending.length == 0">No tasks</div>

        <div class="">Completed ({{ _done.length }})</div>
        <div class="" v-for="item in _done" :key="item.id">
            <label>
                <input type="checkbox" v-model="item.checked">
                <span class="">
                    {{ item.text }}
                </span>
            </label>
        </div>
        <div class="" v-show="_done.length == 0">No tasks</div>

    </div>
</template>

<style scoped>
.item-container {
    max-width: 100%;
    min-width: 30rem;
}

label {
    cursor: pointer;
    display: flex;
}
</style>