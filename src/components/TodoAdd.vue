<script lang="ts">
export default{

  data(){
    return {
      newTodo: '',
      todo: {}
    }
  },
  props: {
    todos:{
      type: Array
    }
  },
  emits: ['addTodo'],
}

</script>



<template>
  <div>
    <label>NewTodo: </label>
    <input v-model="newTodo" class="new-todo" autofocus />
    <button @click="$emit('addTodo',newTodo),newTodo = ''" class="add-todo" > Add </button>
  </div>
</template>

<style scoped>
label{
  position: absolute;
  width: 85px;
  height: 50px;
  left: 250px;
  top: 150px;

  font-size: 40px;
  display: flex;
  align-items: flex-end;
  text-align: center;
}
.new-todo {
  box-sizing: border-box;
  box-shadow: none;
  position: absolute;
  width: 550px;
  height: 50px;
  left: 450px;
  top: 150px;
  font-size: 30px;
  background: #f9f9f9;
  border-radius: 5px;
}
.add-todo {
  cursor: pointer;
  box-shadow: none;
  position: absolute;
  width: 100px;
  height: 50px;
  right: 300px;
  top: 150px;
  font-size: 20px;
  background: #4138C2;
  border-radius: 5px;
  color: var(--color-text);
}

@media (min-width: 1024px) {

}
</style>
