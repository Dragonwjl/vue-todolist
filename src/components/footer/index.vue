<script setup>
import { computed } from '@vue/reactivity';
const { state, filter, listNum } = defineProps(['listNum', 'filter', 'state'])


</script>


<template>
    <footer class="clearfix">
        <div class="pull-left buttons">
            <div>
                <a title="Add New" @click="$emit('changeStatus', 'add', 'btn-left')"
                    :class="[state === 'add' ? 'button add selected'  : 'button add']"></a>
                <a title="Search" @click="$emit('changeStatus', 'search', 'btn-left')"
                    :class="[state === 'search' ? 'button search selected' : 'button search']"></a>
            </div>
        </div>
        <div class="pull-left" id="items">{{ listNum }} items left</div>
        <div class="pull-right">
            <ul class="filters  clearfix">
                <li><a @click="$emit('changeStatus', 'all')"
                        :class="[filter === 'all' ? 'all selected' : 'all']">All</a></li>
                <li><a @click="$emit('changeStatus', 'active')"
                        :class="[filter === 'active' ? 'active selected' : 'active']">Active</a></li>
                <li><a @click="$emit('changeStatus','completed')"
                        :class="[filter === 'completed' ? 'completed selected' : 'completed']">Completed</a></li>
            </ul>
        </div>
       
    </footer>

</template>

<style>
.clearfix:after {
    display: table;
    content: " ";
    clear: both;
}

footer {
    border-top: 1px solid #ddd;
    background-color: #e8e2ca;
    margin: 0 -21px -11px -21px;
    padding: 12px 20px;
    position: relative;
    color: #777;
}

footer .buttons {
    border-right: 1px solid #ccc;
    margin-right: 15px;
    padding-right: 10px;
    height: 20px;
}

.buttons .button {
    display: inline-block;
    margin: 0 5px;
    height: 18px;
    width: 18px;
    cursor: pointer;
    opacity: 0.5;
    transition: 0.3s all;
}

.buttons .button:hover,
.buttons .button.selected {
    opacity: 1;
    border-color: #ddd;
}

.buttons .add {
    background: url(../../assets/add.svg) no-repeat center;
}

.buttons .search {
    background: url(../../assets/search.svg) no-repeat center;
}


.filters {
    margin: 0;
    padding: 0;
    list-style: none;
}

.filters li {
    display: inline-block;
}

.filters li a {
    cursor: pointer;
    color: inherit;
    margin: 3px;
    padding: 4px 8px;
    text-decoration: none;
    border: 1px solid transparent;
    border-radius: 3px;
}

.filters li a.selected,
.filters li a:hover {
    border-color: rgba(175, 47, 47, 0.1);
}

.filters li a.selected {
    border-color: rgba(175, 47, 47, 0.2);
    color: #555;
}


.pull-left {
    float: left !important;
}


.pull-right {
    float: right !important;
}

.clearfix:after {
    display: table;
    content: " ";
    clear: both;
}
</style>