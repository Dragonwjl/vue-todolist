<script setup>
import Header from "./components/header/index.vue"
import Table from "./components/table/index.vue"
import Footer from "./components/footer/index.vue"
import { getLocalStorageData, setLocalStorageData } from "./utils"

let state = $ref({
  status: "add",
  todoList: getLocalStorageData(),
  filter: "all",
  search: '',
  listNum: getLocalStorageData().length
})


const onkeydown = (event) => {
  if (state.status === "add") {
    let data = getLocalStorageData();
    if (event.target.value != '') {
      data.push({ title: event.target.value, done: false, id: data.length })
      state.todoList = data;
      state.listNum = data.length;
    }
    setLocalStorageData(data);
    event.target.value = ''
  }
  else if (state.status === "search") {
    state.search = event.target.value
  }
}


const changeStatus = (value, type) => {
  if (type === "btn-left") {
    state.status =value
    state.search=''
  } else {
    state.filter = value
  }
}

const changeData = (i) => {
  let data = state.todoList
  data[i].done = !data[i].done
  state.todoList = data;
  setLocalStorageData(data)
}

const changeNum = (n) => {
  state.listNum = (n > 0 ? n : 0)
}



</script>

<template>

  <div class="todolist">
    <Header @onkeydown="onkeydown" :state="state.status" />

    <Table @changeNum="changeNum" @changeData="changeData" :listNum="state.listNum" :search="state.search"
      :filter="state.filter" :todoList="state.todoList" />

    <Footer :listNum="state.listNum" @changeStatus="changeStatus" :filter="state.filter" :state="state.status" />

  </div>


</template>

<style scoped>
body {
  background-color: #eee;
  color: #555;
  margin: 0;
  font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 1.42857143;
}



*,
:after,
:before {
  box-sizing: border-box;
}


.todolist {
  background-color: #FFF;
  padding: 20px 20px 10px 20px;
  width: 600px;
  margin: 30px auto;
  border: 1px solid #ddd;
  border-radius: 2px;
  position: relative;
}
</style>
