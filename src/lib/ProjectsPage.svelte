<script>
    import CardProject from "./CardProject.svelte";
    import { URLServer } from "../stores/store";
  let projects = [];
  const getProjects = async () => {
    const res = await fetch(`${$URLServer}/api/get_projects`);
    const data = await res.json();
    projects = data;
  };
  getProjects();
</script>

<div id="container-projects" class="py-4 px-4 flex flex-col gap-4">
    {#each projects as project}
        <CardProject project={project} />
    {/each}
</div>
