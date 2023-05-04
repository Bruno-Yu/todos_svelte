<script>
export let todoList;
export let updateTodo; 

</script>

<section>
  <ul>
    {#each todoList as todo, index (todo.id)}
          <li class="py-4"  data-id={todo.id } >
            <label class={ todo.status ? 'line-through' : ''}>
              <input on:change={ updateTodo } type="checkbox" class="mr-2"  data-id={ todo.id } checked={ todo.status }/>
              { todo.name }
              </label>
            </li>
      {/each}
  </ul>
</section>


<style>
@tailwind base;
@tailwind components;
@tailwind utilities;


</style>