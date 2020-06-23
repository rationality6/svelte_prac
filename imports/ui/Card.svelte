<script>
  export let title;
  export let description;
  export let imageUrl;
</script>

<style>
  .head {
    color: coral;
  }
  .card {
    border-radius: 8px;
    box-shadow: 0 0 4px rgba(255, 0, 0, 0.1);
    max-width: 300px;
    margin: 1rem auto;
  }
  .main_image {
    width: 100%;
    margin-right: 12px;
    vertical-align: middle;
  }
</style>

<div class="card">
  <img class="main_image" src={imageUrl} />
  <h1 class="head">{title}</h1>

  <p>{description}</p>
</div>
