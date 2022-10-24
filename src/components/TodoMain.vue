<template>
    <div class="main">
        <div class="input-group mb-3">
            <input :value="newTodo" @input="onTodoInput" type="text" class="form-control" placeholder="Escribe un quehacer" aria-label="Escribe un quehacer" aria-describedby="basic-addon2">
        </div>
        <div class="input-group mb-3">
            <input :value="newDate" @input="onDateInput" type="text" class="form-control" placeholder="Fecha de vencimiento" aria-label="Fecha de vencimiento" aria-describedby="basic-addon2">
            <div class="input-group-append">
                <button @click="onAddTodo" class="btn btn-outline-secondary" type="button">Agregar</button>
            </div>
        </div>
        <table class="table">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Descripción</th>
                    <th>Fecha</th>
                    <th>Eliminar</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(todo, index) in todos" :key="index">
                    <td :class="todo.isExpired? 'table-danger': 'table-success'">
                        {{ index + 1 }}
                    </td>
                    <td :class="todo.isExpired? 'table-danger': 'table-success'">
                        {{ todo.description }}
                    </td>
                    <td :class="todo.isExpired? 'table-danger': 'table-success'">
                        {{ todo.date }}
                    </td>
                    <td :class="todo.isExpired? 'table-danger': 'table-success'">
                        <svg @click="onDeleteTodo" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16">
                            <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
                            <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
                        </svg>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
  </template>
  
  <script>

  const checkExpired = (date) => {
    const expired = 8.64e+7;
    const now = new Date();
    const itemDate = new Date(date);
    const difference = now - itemDate;
    return difference >=0 || (difference < 0 && Math.abs(difference) < expired);
  };

  export default {
    name: 'TodoMain',
    data() {
        return {
            newTodo: "",
            todos: [],
            newDate: ""
        }
    },
    methods: {
        onTodoInput(e) {
            this.newTodo = e.target.value;
        },
        onDateInput(e) {
            this.newDate = e.target.value;
        },
        onAddTodo() {
            
            this.todos.push({"description": this.newTodo, "date": this.newDate, "isExpired": checkExpired(this.newDate)});
            this.newTodo = "";
            localStorage.setItem(sessionStorage.getItem("user"), JSON.stringify(this.todos));
        },
        onDeleteTodo(e) {
            const rowToDelete = e.target.parentElement.parentElement.children[0].innerText;
            this.todos.splice(rowToDelete-1, 1);
            localStorage.setItem(sessionStorage.getItem("user"), JSON.stringify(this.todos));
        }
    },
    created() {
        let todos = JSON.parse(localStorage.getItem(sessionStorage.getItem("user")));
        if (todos) {
            this.todos = todos.map((item) => {
                /*return {
                    "description": item.description,
                    "date": item.date,
                    "isExpired": checkExpired(item.date)
                }; */
                //equivalentemente
                return {
                    ...item,
                    "isExpired": checkExpired(item.date)
                }
            });
        }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
    .main {
        width:50%;
        margin-left:25%;
    }
  </style>
  