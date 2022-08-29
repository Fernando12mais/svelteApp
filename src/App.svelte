<script lang="ts">
  import TodoList from "./lib/todo-list.svelte";
  import "./app.css";
</script>

<main
  class="px-4 bg-slate-800 min-h-screen flex flex-col justify-center items-center gap-8"
>
  <h1 class="text-5xl text-slate-200 ">To do list</h1>
  <TodoList />
</main>
