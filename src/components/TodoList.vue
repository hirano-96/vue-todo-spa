<script lang = "ts">


export default {
    data() {
        return {
            headers: [
                'No', 'Todo', 'Status', 'Button'
            ],
            status: [
                {Id:0, Name: ''},
                {Id:1, Name: '未着手'},
                {Id:2, Name: '実施中'},
                {Id:3, Name: '完了'}
            ],
        }
    },
    props: {
        todos:{
            type: Array
        }
    },
    methods: {
        getClass(headerName){
            return headerName.toLowerCase()
        },
        getStatus(StatusId){
            return this.status[StatusId].Name
        },
        changeStatus(No,e){
            this.props.todos[No].StatusId = e.target.value
        }
    },
    emits: ['deleteTodo'],
}
</script>

<template>
    <label v-if="this.todos.length==0" class="noTodo">
        Todoがありません
    </label>
    <table v-else>
        <thead>
            <th v-for="header in headers" :key="header" :class="getClass(header)">
                {{ header }}
            </th>
        </thead>
        <tbody >
            <tr v-for="todo in this.todos" :key="todo.No">
                <td>{{ todo.No }}</td>
                <td style="text-align: left;">{{ todo.Todo }}</td>
                <td>
                    <select v-model="todo.StatusId">
                        <option class="sel" v-for="st in status" :key="st.Id">{{ st.Name }}</option>
                    </select>
                </td>
                <td>
                    <button class="del-todo" @click="$emit('deleteTodo', parseInt(todo.No))">Delete</button>
                </td>
            </tr>
        </tbody>
    </table>

</template>

<style scoped>
/* タグに対するスタイル */
label{
    position: relative;
    top: 220px;
    font-size: 30px;
}

table {
    position: relative;
    top: 220px;
    height: fit-content;
    border: 2px solid #4138C2;
    border-radius: 5px;
    background-color: rgba(235, 235, 235, 0.64);
}

thead {
  background-color: #4138C2;
  color: rgba(255, 255, 255, 0.66);
  border-radius: 5px;
  font-size: 20px;
  font:bold;
}

tbody {
    height: 30px;
    border: 2px solid rgb(65, 56, 194);
    border-radius: 5px;
    background-color: rgba(235, 235, 235, 0.64);
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
}

td {
    position: relative;
    background-color: #f9f9f9;
    height: 30px;
    font-size: 15px;
    color: #000000;
    border: none;
    text-align: center;
}
select {
  box-shadow: none;
  width: 150px;
  height: 30px;
  font-size: 15px;
  font: bold;
  text-align: center;
  background: #d9d6c1;
  border-radius: 50px;
  color: #565446;
}

/* classで指定する個別のスタイル */
.no{
  width: 50px;
}
.todo{
  width: 550px;
}
.status{
  width: 200px;
}
.button{
  width: 200px;
}

.del-todo {
  cursor: pointer;
  box-shadow: none;
  width: 100px;
  height: 30px;
  font-size: 15px;
  background: rgb(200, 50, 50);
  border-radius: 5px;
  color: var(--color-text);
}


</style>