<script>
  export let handleFn;
    export let label;
    export let enable=true;

</script>
<label class="p-2 m-2 {enable ? 'bg-indigo-100' : 'bg-red-100'} hover:bg-indigo-200 rounded flex cursor-pointer" class:cursor-not-allowed={!enable}>
  <div><input type="checkbox" on:click={handleFn} disabled={!enable}/></div>
  <div class="ml-2 {enable ? 'text-indigo-900' : 'text-red-400'}">{label}</div>
</label>
