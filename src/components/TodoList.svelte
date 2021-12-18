<script lang="ts">
  export let todos;
  export let updateTodo;
  export let deleteTodo;
  import {
    Checkbox,
    Button,
    Toggle,
    DataTable,
    Row,
    Column,
  } from "carbon-components-svelte";
  import type { Todo } from "../services/todoService";
</script>

<DataTable
  headers={[
    { key: "title", value: "Title" },
    { key: "completed", value: "Completed" },
  ]}
  rows={todos}
>
  <span slot="cell" let:row let:cell>
    {#if cell.key === "completed"}
      <Row>
        <Column
          ><Toggle
            toggled={cell.value}
            on:toggle={(e) => updateTodo(row)}
          /></Column
        >
        <Column
          ><Button kind="danger" on:click={(e) => deleteTodo(row)}>X</Button
          ></Column
        >
      </Row>
    {:else}{cell.value}{/if}
  </span>
</DataTable>

<style>
  
</style>
