<script>
  import { fade } from "svelte/transition";
  import NavBar from "./lib/NavBar.svelte";
  import HomePage from "./lib/HomePage.svelte";
  import ProjectsPage from "./lib/ProjectsPage.svelte";

  import { URLServer, activePage } from "./stores/store";
  import ContactPage from "./lib/ContactPage.svelte";
  URLServer.set(window.location.origin);
  // URLServer.set(`http://${window.location.hostname}:8000`)
</script>

<div class="text-slate-800">
  <NavBar />
  {#if $activePage === "Inicio"}
    <div in:fade={{ delay: 200, duration: 600 }}>
      <HomePage />
    </div>
  {/if}
  
  {#if $activePage === "Proyectos"}
    <div in:fade={{ delay: 200, duration: 600 }}>
      <ProjectsPage />
    </div>
  {/if}
  {#if $activePage === "Contacto"}
    <div in:fade={{delay: 200, duration: 600}}>
      <ContactPage />
    </div>
  {/if}
</div>
