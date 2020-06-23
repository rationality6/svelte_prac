<script>
  import { useTracker } from "meteor/rdb:svelte-meteor-data";
  import { Tasks } from "../api/tasks.js";

  import Task from "./Task";
  import Counter from "./Counter";
  import Card from "./Card";

  $: tasks = useTracker(() =>
    Tasks.find({}, { sort: { createdAt: -1 } }).fetch()
  );

  let newTask = "";

  function handleSubmit(event) {
    Tasks.insert({
      text: newTask,
      createdAt: new Date() // current time
    });

    // Clear form
    newTask = "";
  }

  function getTasks() {
    return [
      {
        _id: 1,
        text: "This is task 1"
      },
      {
        _id: 2,
        text: "This is task 2"
      },
      {
        _id: 3,
        text: "This is task 3"
      },
      { _id: 4, text: "foobar" }
    ];
  }

  function random_gen() {
    return Math.round(Math.random() * 4);
  }

  image_list = [
    "https://mimg.segye.com/content/image/2019/05/18/20190518504340.PNG",
    "https://image.fmkorea.com/files/attach/new/20200211/486616/21412212/2697236936/99b983892094b5c6d2fc3736e15da7d1.jpg",
    "data:image/jpeg;base64,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",
    "https://lh3.googleusercontent.com/proxy/iXD0ychdYeQiKQvp9IE-tQ3TtpjIHBS7TZFbCGs6zihV4lLmWXxJeUn4S_uyY79sFtMKw8TdOoXMa_wbGKrlNEEtBGDfi2mkInipBH9ELxWGuByFWyzPs4XFL7HrTqT0UpW5bkJAiaIrVl0cDLVdpEjy8Av_xWIdR21dryPHbLc",
    "https://lh3.googleusercontent.com/proxy/zw44bqaE5TWGfLP7nrGc_bkhtS2LsSnQU6hsFCJgLrC_7O-oriiO-fPUcEbeY2-dVdnj40V32K2X0JEZpaxde_8INmxkroBmswcaOZwvcjxlcjTMc9gmPVaKThLqwAVxRipTcWsHbWBDFshZ7Kikik4dTDJt9XWp0Xl6QfxOhkC9SBbnq-G1nX75oVwZ_GFzEPVaPFQqqQjKLYCKGecoaPBLFdZlyadINacxNUmg5sJKj19Az21ZSZMRAGkzpzQDxR0-7RRH3H7ZKzIU8RxvZr4ve-HTNjU2Y-_8n1R_f5Y1fgpIzkGrv9pByQ"
  ];
</script>

<style>
  .cards_container {
    display: flex;
    flex-wrap: wrap;
  }
</style>

<div class="container">
  <header>
    <h1>Todo List</h1>

    <form class="new-task" on:submit|preventDefault={handleSubmit}>
      <input
        type="text"
        placeholder="Type to add new tasks"
        bind:value={newTask} />
    </form>

  </header>
  <ul>
    {#each $tasks as task}
      <Task key={task._id} {task} />
    {/each}
  </ul>

  <div>
    <Counter />
  </div>
  <div>
    <Counter />
  </div>

  <div class="cards_container">
    <Card imageUrl={image_list[random_gen()]} title="foo" description="bar" />
  </div>

</div>
