<script lang="ts">
  export let todos;
  import {
    Checkbox,
    Button,
    Toggle,
    DataTable,
    Row,
    Column
  } from "carbon-components-svelte";
  import type { Todo } from "../services/todoService";
</script>


<DataTable headers={[{ key: "title", value: "Title" }, { key: "completed", value: "Completed"}]} rows={todos}>
  <span slot="cell" let:row let:cell>
    {#if cell.key === "completed"}
      <Row>
    <Column><Toggle  toggled={cell.value} on:toggle={(e) => console.log(row)}/></Column>
      <Column><Button kind="danger" on:click={(e) => console.log(row)}>X</Button></Column>
  </Row>
    {:else}{cell.value}{/if}
  </span>
</DataTable>

<style>
  .rowElement {
    display: inline
  }
</style>
