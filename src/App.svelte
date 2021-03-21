<!-- components/Todos.svelte -->
<script>
  export let todos = []
  
  let newTodoName = ''
  $: newTodoId = totalTodos ? Math.max(...todos.map(t => t.id)) + 1 : 1

  $: totalTodos = todos.length
  $: completedTodos = todos.filter(todo => todo.completed).length

  function removeTodo(todo) {
    todos = todos.filter(t => t.id !== todo.id)
  }

  function addTodo() {
    todos = [...todos, { id: newTodoId, name: newTodoName, completed: false }]
    newTodoName = ''
  }

  let filter = 'all'
  const filterTodos = (filter, todos) => 
    filter === 'active' ? todos.filter(t => !t.completed) :
    filter === 'completed' ? todos.filter(t => t.completed) : 
    todos

</script>

<!-- Todos.svelte -->
<div class="max-w-3xl mx-auto mt-11  bg-white rounded shadow-2xl">

  <!-- NewTodo -->
  <form on:submit|preventDefault={addTodo} class="m-4" >
    <h2 class="m-0 flex-initial text-center">
      <label for="todo-0" class="leading-4 font-light
      p-3.5 mb-4 text-center">
        What needs to be done?
      </label>
    </h2>
    <input bind:value={newTodoName} type="text" id="todo-0" autocomplete="off"
     class="p-8 border-2 border-solid 
    border-gray-300 shadow-inner w-full inline-block text-3xl rounded" />
    <button type="submit" disabled="" 
    class="w-full inline-block text-3xl py-3 pr-4 border-b-2 border-solid 
    rounded transition duration-500 ease-in-out bg-green-600 hover:bg-yellow-600
    transform hover:-translate-y-1 hover:scale-100  text-white mt-2 ">
      Add
    </button>
  </form>

  <!-- Filter -->
  <div class="w-full -my-0 flex justify-between mt-5 mx-4 ">
    <button class="rounded transition duration-500 ease-in-out bg-green-600 hover:bg-yellow-600
    transform hover:-translate-y-1 hover:scale-100  py-3 px-4 mr-2 flex-auto text-white toggle-btn" class:btn__primary={filter === 'all'} aria-pressed={filter === 'all'} on:click={()=> filter = 'all'} >
      <span class="absolute w-1 h-1 overflow-hidden">Show</span>
      <span>All</span>
      <span class="absolute w-1 h-1 overflow-hidden">tasks</span>
    </button>
    <button class="rounded py-3 px-4 mr-2 flex-auto transition duration-500 ease-in-out bg-green-600 hover:bg-yellow-600
    transform hover:-translate-y-1 hover:scale-100   text-white toggle-btn" class:btn__primary={filter === 'active'} aria-pressed={filter === 'active'} on:click={()=> filter = 'active'} >
      <span class="absolute w-1 h-1 overflow-hidden">Show</span>
      <span>Active</span>
      <span class="absolute w-1 h-1 overflow-hidden">tasks</span>
    </button>
    <button class="rounded py-3 px-2 mr-8 flex-auto transition duration-500 ease-in-out bg-green-600 hover:bg-yellow-600
    transform hover:-translate-y-1 hover:scale-100  text-white capitalize toggle-btn" class:btn__primary={filter === 'completed'} aria-pressed={filter === 'completed'} on:click={()=> filter = 'completed'} >
      <span class="absolute w-1 h-1 overflow-hidden">Show</span>    
      <span>Completed</span>
      <span class="absolute w-1 h-1 overflow-hidden">tasks</span>
    </button>
  </div>

  <!-- TodosStatus -->
  <h2 id="list-heading" class="px-4 text-center text-4xl font-black text-green-500 capitalize">{completedTodos} out of {totalTodos} items completed</h2>

  <!-- Todos -->
  <ul role="list" class="mx-4 todo-list stack-large" aria-labelledby="list-heading">
  {#each filterTodos(filter, todos) as todo (todo.id)}
    <li class="todo">
      <div class="stack-small">
        <div class="c-cb">
            <input type="checkbox" id="todo-{todo.id}" 
              on:click={() => todo.completed = !todo.completed}
              checked={todo.completed} class="box-border h-12 w-12 p-4 border-4 border-green-500 rounded"
            />          
            <label for="todo-{todo.id}" class="todo-label">
            {todo.name}
          </label>
        </div>
        <div class="w-full -my-0 flex justify-between mt-5 mx-4">
          <button type="button" class="rounded transition duration-500 ease-in-out bg-green-600 hover:bg-yellow-600
          transform hover:-translate-y-1 hover:scale-100  py-3 px-4 mr-2 flex-auto text-white toggle-btn">
            Edit <span class="absolute w-1 h-1 overflow-hidden">{todo.name}</span>
          </button>
          <button type="button" class="rounded transition duration-500 ease-in-out bg-green-600 hover:bg-red-600
          transform hover:-translate-y-1 hover:scale-100  py-3 px-4 mr-2 flex-auto text-white toggle-btn"
            on:click={() => removeTodo(todo)}
          >
            Delete <span class="absolute w-1 h-1 overflow-hidden">{todo.name}</span>
          </button>
        </div>
      </div>
    </li>
  {:else}
    <li>Nothing to do here!</li>
  {/each}
  </ul>

  <hr />

  <!-- MoreActions -->
  <div class="btn-group">
    <button type="button" class="btn btn__primary">Check all</button>
    <button type="button" class="btn btn__primary">Remove completed</button>
  </div>

</div>