<script>
async function getTodo() {
  const randomId = Math.floor(Math.random() * (100 + 1 - 1)) + 1;
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${randomId}`
  );
  const json = await res.json();

  if (res.ok) {
    return json;
  } else {
    throw new Error(res.status);
  }
}

let promise = getTodo();

function handleClick() {
  promise = getTodo();
}
</script>

<button on:click="{handleClick}"> get todo </button>

<!-- replace this element -->
{#await promise}
  <p>...waiting</p>
{:then todo}
  <p>The todo id is {todo.id}</p>
  <p>The todo title is {todo.title}</p>
{:catch error}
  <p style="color: red">{error}</p>
{/await}
