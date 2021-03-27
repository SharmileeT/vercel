<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()
    export let todo
    let editing = false
    let name = todo.name
    let checked = false;
   
    function update(updatedTodo) {
        todo ={...todo,...updatedTodo}
        dispatch('update',todo)
    }

    function onCancel() {
        name=todo.name
        editing =false
    }

    function onSave() {
        update({name:name})
        if(checked !== todo.completed)
            update({completed:!todo.completed})
        editing = false
    }

    function onEdit() {
        editing =true
        checked=todo.completed
    }

    function onToggle() {
        checked=!checked
        
    }
</script>

<tr class="border-b border-gray-200 hover:bg-gray-100">
    {#if editing}
    <td class="py-3 px-6 text-left whitespace-nowrap">
        <div class="flex ">
          <input class="p-2 flex-grow-0 w-full" bind:value={name}/>
        </div>
    </td>
    <td class="py-3 px-6 text-center whitespace-nowrap">            
        <label for="unchecked" class="mt-3 inline-flex items-center cursor-pointer">
            <span class="relative">
              <span class:checkedOuter={checked} class="block w-24 h-6 bg-red-200 rounded-full shadow-inner text-red-600">{checked? 'Completed' : 'Pending'}</span>
              <span class:checked={checked} class="absolute block w-4 h-4 mt-1 ml-1 bg-red-600 rounded-full shadow inset-y-0 left-0 focus-within:shadow-outline transition-transform duration-500 ease-in-out">
                <input id="unchecked"  on:click={onToggle} checked={todo.completed} type="checkbox" class="absolute opacity-0 w-0 h-0" />
              </span>
            </span>
          
          </label>
         
    </td>
    <td class="py-3 px-6 text-center">
        <div class="flex item-center justify-center">
    
            <div class="w-4 mr-2 transform hover:text-purple-500 hover:scale-110" on:click={()=>onCancel()}>
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" 
                fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                class="feather feather-x-circle"><circle cx="12" cy="12" r="10"></circle><line x1="15" y1="9" x2="9" y2="15"></line><line x1="9" y1="9" x2="15" y2="15"></line></svg>
            </div>
            <div class="w-4 mr-2 transform hover:text-purple-500 hover:scale-110" on:click={() => onSave()}>
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-save"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"></path><polyline points="17 21 17 13 7 13 7 21"></polyline><polyline points="7 3 7 8 15 8"></polyline></svg>
            </div>
        </div>
    </td>
    {:else}
    <td class="py-3 px-6 text-left whitespace-nowrap">
        <div class="flex items-center">
          <span class="font-medium">{todo.name}</span>
        </div>
    </td>
    <td class="py-3 px-6 text-center">
      <span class="bg-red-200 text-red-600 py-1 px-3 rounded-full text-xs" class:completed={todo.completed}>{todo.completed? 'Completed' : 'Pending'}</span>
    </td>
    <td class="py-3 px-6 text-center">
    <div class="flex item-center justify-center">

        <div class="w-4 mr-2 transform hover:text-purple-500 hover:scale-110" on:click={()=> onEdit()}>
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z" />
            </svg>
        </div>
        <div class="w-4 mr-2 transform hover:text-purple-500 hover:scale-110" on:click={() => dispatch('remove',todo)}>
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
            </svg>
        </div>
    </div>
</td>
{/if}
</tr>