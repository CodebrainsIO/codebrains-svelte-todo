<script lang="ts">
  import "carbon-components-svelte/css/white.css";
  import { onMount } from "svelte";

  import { DataTable, Link } from "carbon-components-svelte";
  import TodoForm from "./components/TodoForm.svelte";
  import { todos } from "./services/store";
  import { createTodo, loadTodos, updateTodo } from "./services/todoService";
import TodoList from "./components/TodoList.svelte";

  onMount(async () => {
    todos.set(await loadTodos());
  });
  const getTodos = async () => {
    return await loadTodos();
  };

  const submitTodo = async (todo) => {
    await createTodo(todo);
    await loadTodos();
  };

  const updateStatus = async (todo) => {
    await updateTodo(todo);
    await loadTodos();
  };
</script>

<main>
  <h2>Codebrains Todos</h2>
  <TodoForm />
  <TodoList todos={$todos} />
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
