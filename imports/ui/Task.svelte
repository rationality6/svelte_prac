<script>
  import { Tasks } from "../api/tasks.js"

  export let key;
  export let task;

  function toggleChecked() {
    // Set the checked property to the opposite of its current value
    Tasks.update(task._id, {
      $set: { checked: !task.checked }
    });
  }

  function deleteThisTask() {
    Tasks.remove(task._id);
  }
</script>

<li class:checked={task.checked}>
  <button class="delete" on:click={deleteThisTask}>X</button>

  <input
    type="checkbox"
    readonly
    checked={!!task.checked}
    on:click={toggleChecked} />

  <span class="text">{task.text}</span>
  <span>{task.createdAt}</span>
</li>
