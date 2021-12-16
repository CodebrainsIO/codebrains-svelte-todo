<script>
  import {
    Form,
    FormGroup,
    TextInput,
    Button,
    Grid,
    Row,
    Column,
  } from "carbon-components-svelte";
  import { todos } from "../services/store";
  import { createTodo, loadTodos, updateTodo } from "./services/todoService";
  let title = '';
  $: disabled = title.length < 3;
  const submit = async () => {
      console.log({title: title, completed: false});
      todos.set(await loadTodos());
      title = '';
  }
</script>

<Grid>
  <Row>
      <Column>
        <TextInput placeholder="Enter Todo..." bind:value={title}/>
      </Column>
      <Column>
        <Button type="submit" on:click={submit} disabled={disabled}>Add</Button>
      </Column>
  </Row>
</Grid>

<style>
</style>
