<script lang="ts">
  let tasks: { name: string; isDone: boolean }[] = [
    ...(JSON.parse(localStorage.getItem("tasks")) || []),
  ];
  let inputValue = "";
  $: tasks && localStorage.setItem("tasks", JSON.stringify(tasks));
  import { Trash3Fill, CheckCircleFill } from "svelte-bootstrap-icons";
</script>

<div class="p-3 border-2 border-cyan-500 rounded-lg flex flex-col gap-4">
  <form
    class="flex flex-col gap-4"
    on:submit={(e) => {
      e.preventDefault();
      tasks = [...tasks, { name: inputValue, isDone: false }];
      inputValue = "";
    }}
  >
    <label
      class="text-base items-center uppercase font-bold text-slate-300 flex gap-2 flex-col sm:flex-row"
    >
      Add task
      <input
        bind:value={inputValue}
        required
        class="rounded outline-none text-slate-800 text-base p-1 bg-slate-100"
      />
    </label>
    <button
      class="bg-green-600 p-2 uppercase text-slate-200 font-bold rounded-md hover:bg-green-300 hover:text-slate-800"
      >Add new task</button
    >
  </form>
  <p class="text-xl font-bold text-green-500">Tasks</p>

  <table>
    <tr>
      <th
        class="border-2  rounded-l-lg border-slate-800 bg-slate-100 text-slate-800 uppercase"
        >task name</th
      >
      <th
        class="border-2 px-2 rounded-r-lg border-slate-800 bg-slate-100 text-slate-800 uppercase"
        >Actions</th
      >
    </tr>

    {#each tasks as task, index}
      <tr>
        <input
          bind:value={task.name}
          class="w-full border-b-2 rounded-l-md border-slate-800 bg-slate-100 text-slate-800 uppercase text-center px-1 outline-none"
        />
        <td
          class="border-2  rounded-r-lg border-slate-800 bg-slate-100 text-slate-800 uppercase"
        >
          <div class="flex gap-4 items-center justify-around ">
            <button
              on:click={() => {
                tasks = tasks.filter((task, newIndex) => index !== newIndex);
              }}><Trash3Fill class="fill-red-400" /></button
            >

            <button
              on:click={() => (tasks[index].isDone = !tasks[index].isDone)}
              ><CheckCircleFill
                class={`${task.isDone ? "fill-cyan-600" : "fill-gray-600"}`}
              /></button
            >
          </div>
        </td>
      </tr>
    {/each}
  </table>
</div>
