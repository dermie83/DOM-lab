<script>
import { v4 as uuidv4 } from 'uuid';
import Title from "./Title.svelte";
import TodoList from "./TodoList.svelte";
import AddTodoForm from "./AddTodoForm.svelte";

  let todoText = "";
  let todoItems = [];
  let doneItems = [];

  function addTodo(todoText) {
    const todo = {
      text: todoText,
      date: new Date().toLocaleString("en-IE"),
      id: uuidv4(),
    };
    console.log(todo)
    todoItems.push(todo);
    todoItems = [...todoItems];
    todoText = "";
  }

  // function uuidv4() {
  //   return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(/[xy]/g, function (c) {
  //     var r = Math.random() * 16 | 0, v = c == "x" ? r : (r & 0x3 | 0x8);
  //     return v.toString(16);
  //   });
  // }

  function deleteTodo(id) {
    const found = todoItems.findIndex((todo) => todo.id == id);
    const done = todoItems[found];
    todoItems.splice(found, 1);
    todoItems = [...todoItems];
    doneItems.push(done);
    doneItems = [...doneItems];
  }
</script>

<div class="container">
  <Title title="Simple Todo List" subTitle="Fun Things to do"/>
  <div class="section box">
    <AddTodoForm addTodo="{addTodo}" />
  </div>
  <TodoList caption="Items Todo" items="{todoItems}" deleteHandler="{deleteTodo}"/>
  <TodoList caption="Items Done" items="{doneItems}"/>
</div>
