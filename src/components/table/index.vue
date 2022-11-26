<script setup>
import { computed } from '@vue/reactivity';
import { onMounted, watch, watchPostEffect } from 'vue';
const emit = defineEmits(['changeNum', 'changeData'])

const { todoList, filter, listNum, search } = defineProps(["todoList", "filter", "search", "listNum"])

const datas =
    computed(
        () =>
            todoList.filter((data) => {
                if (filter === "all") {
                    return data && data.title.includes(search)
                } else if (filter === "active") {
                    return data.done === false && data.title.includes(search)
                } else if (filter === "completed") {
                    return data.done === true && data.title.includes(search)
                }
            })
    )

watchPostEffect(() => {
    emit('changeNum', datas.value.length)

})

</script>


<template>
    <ul class="list-unstyled">
        <li v-for="value in datas" :key="value.id" class="todo-item ui-state-default pending ">
            <div class="checkbox">
                <label :style="value.done === true ? { textDecoration: 'line-through', color: '#aaa' } : null">
                    <input type="checkbox" @click="emit('changeData', value.id)" :checked="value.done" />
                    {{ value.title }}
                </label>
            </div>
        </li>
    </ul>
</template>

<style>
li.ui-state-default {
    background: #fff;
    border: none;
    border-bottom: 1px solid #ddd;
}

li.ui-state-default:last-child {
    border-bottom: none;
}

li.completed label {
    text-decoration: line-through;
    color: #aaa;
}

li {
    list-style: none;
}

ul {
    padding-inline-start: 0px;
}


a {
    color: #337ab7;
    text-decoration: none;
}
</style>