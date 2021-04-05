<template>
    <div class="list-group">
        <p href="#" class="list-group-item list-group-item-action active">
            Todo List
        </p>
        <input type="text" placeholder="Type Todo Here" class="input-group-text" v-model="todo" @keyup.enter="addTodo">
        <button type="button" class="btn btn-primary button-submit" @click="addTodo()">Add Todo
        </button>

            <table class="table-todo" v-if="todos.length >0">
                <tr>
                    <th scope="col">~</th>
                    <th scope="col">Todo</th>
                    <th scope="col">Action</th>
                </tr>
                <tbody v-for="(todo, index) in todos" :key="index">
                    <td scope="row">{{ index }}</td>
                    <td>{{ todo }}</td>
                    <td>
                        <button class="btn btn-danger" @click="deleteTodo(index)">Delete</button>
                    </td>
                </tbody>
            </table>
            <h4 v-else class="empty-todo">Todo's Empty</h4>
        </div>
</template>

<script>
export default {
    data() {
        return {
            todos: [],
            todo: ""
        }
    },
    methods: {
        addTodo() {
            this.todos.push(this.todo);
            this.todo = " ";
        },
        deleteTodo(index) {
            this.todos.splice(index, 1);
        }
    },
    watch: {
        todos() {
            localStorage.setItem("todos", JSON.stringify(this.todos));
            console.log('Todos Added')
        }
    }
}
</script>

<style>
.list-group {
    width: 400px;
    margin: auto;
    margin-top: 160px;
}
.list-group-item {
    text-align: center;
    box-shadow: 6px 6px 9px #39cccc;
}
.input-group-text {
    height: 40px;
    box-shadow: 3px 3px 3px cyan;
    background-color: white;
}
.button-submit {
    width: 100px;
    margin: auto;
    margin-top: 20px;
}
.empty-todo {
    text-align: center;
    margin-top: 30px;
}
.table-todo {
    text-align: center;
    margin-top: 30px;
}
</style>