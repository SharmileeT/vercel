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
</style>