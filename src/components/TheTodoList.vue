<template>
  <div class="todo-list">
    <h3>Todo List</h3>
    <input type="text" class="input-new-item" v-on:keyup.enter="addNewItemToList">

    <ul>
      <li v-for="(item, index) in list" :key="index">
        <span class="list-item">
        <input type="checkbox" :id="index" class="item-checkbox" v-model="item.checked">
        <label :for="index" :class="getItemClass(item.checked)">{{ item.label }}</label>
        </span>
        <span v-html="deleteIcon" @click="deleteItem(index)"></span>
      </li>
    </ul>
  </div>
</template>

<script>
import feather from 'feather-icons'

export default {
  name: 'TheTodoList',
  data(){
    return {
      list: [],
    }
  },
  created(){
      const itensInLocalStorage = JSON.parse(localStorage.getItem('list'));
      this.list = itensInLocalStorage ? itensInLocalStorage : []
  },
  computed: {
    deleteIcon(){
      return feather.icons.trash.toSvg({'width': 15})
    }
  },
  methods: {

    getItemClass(itemChecked){
      return itemChecked ? 'item-checked' : ''
    },
    addNewItemToList(event){
      const newItem = event.target.value
      this.list.unshift({ label: newItem, checked: false })
      this.uptadeLocalStorage()
      event.target.value = "";
    },
    deleteItem(index){
      this.list.splice(index, 1)
      this.uptadeLocalStorage()

    },
    uptadeLocalStorage(){
      localStorage.setItem('list', JSON.stringify(this.list))
    }
  }
}
</script>


<style scoped>

.todo-list {
  width: 500px;
  margin: auto;
}

.input-new-item {
  widows: 80%;
  height: 30px;
}

ul {
  list-style: none;
  padding: 0;
  width: 80%;
  margin: 20px auto;
  text-align: left;
}

li, .list-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.item-checkbox {
  margin-right: 10px;
}

.item-checked {
  text-decoration: line-through;
}

.todo-list input.input-new-item {
  outline: 0;
  border-radius: 3px;
  border: none;
  padding: 0 5px 0;
}

span.list-item input.item-checkbox {
  cursor: pointer;
}


</style>
   