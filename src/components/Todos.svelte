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
    function onKeydown(event) {   
    if (event.key === "Enter") {
      addTodo()
    }
  }
  
    let filter = 'All'
    const filterTodos = (filter, todos) => 
      filter === 'Active' ? todos.filter(t => !t.completed) :
      filter === 'Inactive' ? todos.filter(t => t.completed) : 
      todos
      let selected;
  </script>
  
  <!-- Todos.svelte -->
  <div class="overflow-x-auto">
    <div class="min-w-screen min-h-screen bg-gray-100 flex items-center justify-center  font-sans overflow-hidden">
        <div class="w-full lg:w-5/6">
            <div class="bg-white shadow-md rounded my-6">
    <!-- NewTodo -->
              <div class="m-1">
                <h2 class="m-0 flex-initial text-center">
                  <label for="todo-0" class="leading-4 font-light
                  p-3.5 mb-4 text-center">
                    What needs to be done?
                  </label>
                </h2>
                <div class="mt-4">
                    <input bind:value={newTodoName} class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker" placeholder="Add Todo(hit enter to add to list)" on:keydown={onKeydown}>
                
                </div>
            </div>
  
  
  
  
    <!-- Filter -->
    <div class="w-1/4">
      <select bind:value={selected} on:change={()=> filter = selected}
          class="m-1 h-full rounded border-t  border-r border-b block appearance-none w-full bg-white border-gray-400 text-gray-700 py-2 px-4 pr-8 leading-tight focus:outline-none focus:border-l focus:border-r focus:bg-white focus:border-gray-500">
          <option >All</option>
          <option >Active</option>
          <option >Inactive</option>
      </select>
  
    </div>
    <!-- TodosStatus -->
    <table class="min-w-max w-full table-auto">
      <thead>
          <tr class="bg-gray-200 text-gray-600 uppercase text-sm leading-normal">
              <th class="py-3 px-6 text-left">Todo</th>         
              <th class="py-3 px-6 text-center">Status</th>
              <th class="py-3 px-6 text-center">Actions</th>
          </tr>
      </thead>
      <tbody class="text-gray-600 text-sm font-light">
    {#each filterTodos(filter, todos) as todo (todo.id)}
      
    <tr class="border-b border-gray-200 hover:bg-gray-100">
      <td class="py-3 px-6 text-left whitespace-nowrap">
          <div class="flex items-center">
            <span class="font-medium">{todo.name}</span>
          </div>
      </td>
      <td class="py-3 px-6 text-center">
        <span class="bg-red-200 text-red-600 py-1 px-3 rounded-full text-xs" class:completed={todo.completed}>status</span>
    </td>
    <td class="py-3 px-6 text-center">
      <div class="flex item-center justify-center">
          <div class="w-4 mr-2 transform hover:text-purple-500 hover:scale-110">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
              </svg>
          </div>
          <div class="w-4 mr-2 transform hover:text-purple-500 hover:scale-110">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z" />
              </svg>
          </div>
          <div class="w-4 mr-2 transform hover:text-purple-500 hover:scale-110" on:click={() => removeTodo(todo)}>
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
              </svg>
          </div>
      </div>
  </td>
  </tr>
    {/each}
      </tbody>
    </table>
  
    <hr />
  
    <!-- MoreActions -->
    <div class="btn-group">
      <button type="button" class="btn btn__primary">Check all</button>
      <button type="button" class="btn btn__primary">Remove completed</button>
    </div>
  
  </div>
        </div>
    </div>
  </div>