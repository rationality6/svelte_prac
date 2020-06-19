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

  image_list = [
    "https://mimg.segye.com/content/image/2019/05/18/20190518504340.PNG"
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
    <Card imageUrl={image_list} title="foo" description="bar" />
    <Card imageUrl={image_list} title="foo" description="bar" />
    <Card imageUrl={image_list} title="foo" description="bar" />
    <Card imageUrl={image_list} title="foo" description="bar" />
    <Card imageUrl={image_list} title="foo" description="bar" />
    <Card imageUrl={image_list} title="foo" description="bar" />
  </div>

</div>
