<script>
  import { onMount } from "svelte";

  let name = "User";
  let todos = [];
  let todoText = "";
  onMount(() => {
    const existingTodos = localStorage.getItem("todos");
    todos = JSON.parse(existingTodos) || [];
  });
  function addTodo(e) {
    e.target[0].value = "";
    todos = [...todos, todoText];
    localStorage.setItem("todos", JSON.stringify(todos));
  }
</script>

<main>
  <h1>Hello {name}!</h1>
  <form on:submit|preventDefault={addTodo}>
    <input bind:value={todoText} />
    <input type="submit" value="Add todo" />
  </form>
  <ul>
    {#each todos as todo}
      <li>{todo}</li>
    {/each}
  </ul>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
