<script>
 let openTab = 1;
 function toggleTabs(tabNumber){
   openTab = tabNumber
 }
 export let labels = [];

</script>

<div class="max-w-7xl mx-auto flex flex-wrap">
  <div class="w-full flex flex-column">
    <ul class="mr-2 list-none w-1/4">
      {#each labels as label, i}
      <li class="my-2 text-center">
        <button type="button" class="w-full text-xs  px-5 py-2 shadow hover:shadow-lg rounded block leading-normal {openTab === i+1 ? 'text-white bg-gray-600':'text-gray-600 bg-white'}" on:click={() => toggleTabs(i+1)}>
	  <span>{label}</span>
        </button>
      </li>
      {/each}
    </ul>
    <div class="relative flex flex-col min-w-0 break-words bg-white w-full mb-6 shadow-lg rounded">
      <div class="px-4 py-5 flex-auto">
        <div class="tab-content tab-space">
          <div class="{openTab === 1 ? 'block':'hidden'}">
	    <slot name="tab1"></slot>
          </div>
          <div class="{openTab === 2 ? 'block':'hidden'}">
	    <slot name="tab2"></slot>
          </div>
          <div class="{openTab === 3 ? 'block':'hidden'}">
	    <slot name="tab3"></slot>
          </div>
          <div class="{openTab === 4 ? 'block':'hidden'}">
	    <slot name="tab4"></slot>
          </div>
          <div class="{openTab === 5 ? 'block':'hidden'}">
	    <slot name="tab5"></slot>
          </div>
          <div class="{openTab === 6 ? 'block':'hidden'}">
	    <slot name="tab6"></slot>
          </div>
          <div class="{openTab === 7 ? 'block':'hidden'}">
	    <slot name="tab7"></slot>
          </div>
          <div class="{openTab === 8 ? 'block':'hidden'}">
	    <slot name="tab8"></slot>
          </div>
          <div class="{openTab === 9 ? 'block':'hidden'}">
	    <slot name="tab9"></slot>
          </div>
          <div class="{openTab === 10 ? 'block':'hidden'}">
	    <slot name="tab10"></slot>
          </div>
          <div class="{openTab === 11 ? 'block':'hidden'}">
	    <slot name="tab11"></slot>
          </div>
          <div class="{openTab === 12 ? 'block':'hidden'}">
	    <slot name="tab12"></slot>
          </div>
          <div class="{openTab === 13 ? 'block':'hidden'}">
	    <slot name="tab13"></slot>
          </div>
          <div class="{openTab === 14 ? 'block':'hidden'}">
	    <slot name="tab14"></slot>
          </div>
          <div class="{openTab === 15 ? 'block':'hidden'}">
	    <slot name="tab15"></slot>
          </div>
          <div class="{openTab === 16 ? 'block':'hidden'}">
	    <slot name="tab16"></slot>
          </div>
          <div class="{openTab === 17 ? 'block':'hidden'}">
	    <slot name="tab17"></slot>
          </div>
          <div class="{openTab === 18 ? 'block':'hidden'}">
	    <slot name="tab18"></slot>
          </div>
          <div class="{openTab === 19 ? 'block':'hidden'}">
	    <slot name="tab19"></slot>
          </div>
          <div class="{openTab === 20 ? 'block':'hidden'}">
	    <slot name="tab20"></slot>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
