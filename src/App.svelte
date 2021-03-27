<!-- App.svelte -->
<script>
  import Todos from './components/Todos.svelte'

  let todos = [
    { id: 1, name: 'Create a Svelte starter app', completed: true },
    { id: 2, name: 'Create your first component', completed: true },
    { id: 3, name: 'Complete the rest of the tutorial', completed: false }
  ]
</script>

<Todos {todos} />
<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  
  .completed{
    @apply bg-green-200 text-green-600 py-1 px-3 rounded-full text-xs;
  }
 
  .checked
  {
@apply absolute block w-4 h-4 mt-1 ml-1 rounded-full shadow inset-y-0 left-0  transition-transform duration-300 ease-in-out bg-green-600 transform translate-x-full;
  }

  .checkedOuter
  {
    @apply block w-28 h-6  bg-green-200 rounded-full shadow-inner text-green-600;
  }



  
  
</style>