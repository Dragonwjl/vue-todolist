<script setup>
const {state} = defineProps(["state"])

</script>

<template>
    <header>
        <h1 class="title">To Do Tasks</h1>
        
        <input v-if="state==='add'" type="text" @keyup.enter="$emit('onkeydown', $event)" class="form-control add-input"
            placeholder="Add New" required />

            <input v-else-if="state==='search'" type="text" @keyup.enter="$emit('onkeydown', $event)"  class="form-control search-input" placeholder="Srearch" required />
    </header>
</template>

<style>
.title {
    margin: 0;
    padding-bottom: 20px;
    text-align: center;
    text-transform: uppercase;
}


.form-control {
    width: 100%;
    height: 34px;
    background-color: #fff;
    background-image: none;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-shadow: inset 0 1px 1px rgb(0 0 0 / 8%);
    transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out;
}


.form-control:focus {
    border-color: #66afe9;
    outline: 0;
    box-shadow: inset 0 1px 1px rgb(0 0 0 / 8%), 0 0 8px rgb(102 175 233 / 60%);
}
</style>