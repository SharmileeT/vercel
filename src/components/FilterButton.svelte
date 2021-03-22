<script>
    export let filter ='All'
    let selected;
</script>

<div class="w-1/4">
    <select bind:value={selected} on:change={()=> filter = selected}
        class="m-1 h-full rounded border-t  border-r border-b block appearance-none w-full bg-white border-gray-400 text-gray-700 py-2 px-4 pr-8 leading-tight focus:outline-none focus:border-l focus:border-r focus:bg-white focus:border-gray-500">
        <option >All</option>
        <option >Active</option>
        <option >Inactive</option>
    </select>

  </div>