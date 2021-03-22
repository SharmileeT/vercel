<!-- components/Todos.svelte -->
<script>
    import FilterButton from './FilterButton.svelte'
    import Todo from './Todo.svelte'
    
      export let todos = []
     
      let newTodoName = ''
      $: newTodoId = totalTodos ? Math.max(...todos.map(t => t.id)) + 1 : 1
    
      $: totalTodos = todos.length
      $: completedTodos = todos.filter(todo => todo.completed).length
    
     
      function addTodo() {
        console.log({newTodoName})
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
     
        function removeTodo(todo) {
          todos = todos.filter(t => t.id !== todo.id)
      }
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
    <FilterButton bind:filter={filter}/> 
    
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
        
    <Todo bind:todo ={todo} on:remove={e=>removeTodo(e.detail)}/>
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