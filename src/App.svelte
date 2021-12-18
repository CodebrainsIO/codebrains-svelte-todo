<script lang="ts">
  import "carbon-components-svelte/css/white.css";
  import { onMount } from "svelte";

  import { DataTable, Link } from "carbon-components-svelte";
  import TodoForm from "./components/TodoForm.svelte";
  import { todos } from "./services/store";
  import { createTodo, loadTodos, updateTodo, deleteTodo } from "./services/todoService";
import TodoList from "./components/TodoList.svelte";

  onMount(async () => {
    todos.set(await loadTodos());
  });
  const getTodos = async () => {
    return await loadTodos();
  };

  const submitTodo = async (todo) => {
    await createTodo(todo);
    todos.set(await loadTodos());
  };

  const updateStatus = async (todo) => {
    let updatedTodo = { ...todo, completed: !todo.completed };
    console.log("Update Todo Status: ", updatedTodo);
    await updateTodo(updatedTodo);
    todos.set(await loadTodos());
  };

  const deleteTodoItem = async (todo) => {
    await deleteTodo(todo.id);
    todos.set(await loadTodos());
  };
</script>

<main>
  <h2>Codebrains Todos</h2>
  <TodoForm submitTodo={submitTodo}/>
  <TodoList todos={$todos} updateTodo={updateStatus} deleteTodo={deleteTodoItem} />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
