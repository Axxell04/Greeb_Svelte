<script>
  import { fade } from "svelte/transition";
  import { URLServer } from "../stores/store";
  export let project;
</script>

<div class="bg-slate-800 rounded-md px-2 py-2 flex flex-col gap-3 md:flex-row">
  <div class="flex flex-col gap-2 md:max-w-60 lg:max-w-80 md:px-3 md:py-3">
    <span class="text-lime-400 text-xl font-bold">{project.name}</span>
    <span class="text-lime-200 font-light md:font-normal"
      >{project.description}</span
    >
  </div>
  <div class="flex flex-col gap-2 justify-items-center w-full md:py-3 md:px-3">
    {#if project.imgs}
      {#each project.imgs as img}
        <img
          in:fade={{ delay: 200, duration: 600 }}
          class="place-self-center rounded-md max-h-96"
          src={`${$URLServer}${img.src}`}
          loading="lazy"
          alt=""
          srcset=""
        />
      {/each}
    {/if}
  </div>
</div>
