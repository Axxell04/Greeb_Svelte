<script>
    import {activePage} from "../stores/store"
    const selectActivePage = (name="") => {
        activePage.set(name);
    }
</script>


<header class=" px-5 font-bold bg-slate-800 flex flex-col">
    <div class="logo flex-1 text-5xl text-lime-400 py-2 align-middle italic">Greeb</div>
    <div class="flex gap-3 justify-end italic">
        <button class="text-lime-200 {$activePage === "Inicio" ? "border-b-4": ""} border-lime-400 px-1 hover:text-lime-600" on:click={() => selectActivePage("Inicio")}>Inicio</button>
        <button class="text-lime-200 px-1 {$activePage === "Proyectos" ? "border-b-4": ""} border-lime-400 hover:text-lime-600" on:click={() => selectActivePage("Proyectos")}>Proyectos</button>
        <button class="text-lime-200 px-1 {$activePage === "Contacto" ? "border-b-4": ""} border-lime-400 hover:text-lime-600" on:click={() => selectActivePage("Contacto")}>Contacto</button>
    </div>
</header>