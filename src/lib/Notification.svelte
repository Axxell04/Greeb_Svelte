<script>
    export let type;
    export let title;
    export let message;
</script>

<div class="absolute {type === "Success" ? "bg-lime-400" : "bg-red-400"}  px-4 py-2 bottom-0 w-full">
    <p class="text-slate-800 font-medium text-center">{title}</p>
    <p class="text-slate-800 text-center">{message}</p>
</div>