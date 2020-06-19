<script>
  import Task from "./Task";
  import Counter from "./Counter";
  import Card from "./Card";

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
</script>

<div class="container">
  <header>
    <h1>Todo List</h1>
  </header>
  <ul>
    {#each getTasks() as task}
      <Task key={task._id} {task} />
    {/each}
  </ul>

  <div>
    <Counter />
  </div>
  <div>
    <Counter />
  </div>

  <Card title="foo" description="bar" />

</div>
