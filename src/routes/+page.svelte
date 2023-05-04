<section>
  <div>
    <div class="bg-indigo-500 p-5 h-screen">
        <div class="max-w-[768px] m-auto bg-white p-5">
          <h1 class="text-center text-2xl mb-4">Svelte ToDoList</h1>
          <div class="flex">
            <input id="todoInput" type="text" class="w-full rounded-l-lg border-l-2 border-y-2 border-indigo-300 pl-4 focus:outline-indigo-500 focus:outline-none focus:outline-offset-0" placeholder="請輸入你的代辦事項 " bind:value={input} />
            <button on:click={ addTodo } class="w-[50px] h-[50px] border-0 bg-sky-500 hover:bg-sky-600 rounded-r-lg text-white transition duration-700">+</button>
          </div>
          <!-- todoList -->
            <List {todoList} {updateTodo}/>
          <div class="flex justify-between items-center">
            <p>
              目前有 <span class="font-medium">{ todoList.length }</span> 個事項待完成
            </p>

            <button on:click={ remoteAllTodo } type="button" class="bg-red-300 p-2 rounded-md hover:bg-red-400 transition duration-700">Clear All Todo</button>
          </div>
        </div>
      </div>
  </div>
</section>


<script>
   import List from './components/List.svelte';
  import { onMount } from 'svelte';
  let todoList = [];
  let input ='';

 const addTodo = (event) => {
     todoList= [ ...todoList,  {
        id: Date.now(),
        name: input,
        status: false,
      }]
    input = '';
  };
const updateTodo = (event) => {
    const { id } = event.target.dataset;
    const newTodoList = todoList.map((todo) => {
      if(todo.id === Number(id)) {
        todo.status = !todo.status;
      }
      return todo;
    });
      todoList=([...newTodoList]);
  }

  const remoteAllTodo = () => {
    todoList=[];
  };
  
  onMount(()=>{
    todoList = JSON.parse( window.localStorage.getItem('todoList')) ||  [];
  })

</script>


<style>
@tailwind base;
@tailwind components;
@tailwind utilities;



</style>
