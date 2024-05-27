<script>
    import {activePage} from "../stores/store"
    const selectActivePage = (name="") => {
        activePage.set(name);
    }
</script>


<header class=" px-5 font-bold bg-slate-800 flex flex-col">
    <div  class="logo relative flex flex-1 flex-row  py-2 align-middle "><span class="z-10 pt-3 italic text-5xl font-extrabold -rotate-12 text-lime-400">Greeb</span><img class="w-28 left-3 absolute" src="static/dist/greeb1.2.png" alt="" srcset=""></div>
    <div class="flex gap-3 justify-end italic">
        <button class="text-lime-200 {$activePage === "Inicio" ? "border-b-4": ""} border-lime-400 px-1 hover:text-lime-600" on:click={() => selectActivePage("Inicio")}>Inicio</button>
        <button class="text-lime-200 px-1 {$activePage === "Proyectos" ? "border-b-4": ""} border-lime-400 hover:text-lime-600" on:click={() => selectActivePage("Proyectos")}>Proyectos</button>
        <button class="text-lime-200 px-1 {$activePage === "Contacto" ? "border-b-4": ""} border-lime-400 hover:text-lime-600" on:click={() => selectActivePage("Contacto")}>Contacto</button>
    </div>
</header>