<script>
    import { onMount } from "svelte";
    import Buscar from "./Buscar.svelte";

    let data = [];
    let datosFiltrados = [];
    let busqueda = "";

    async function getArticulos() {
        const response = await fetch(`https://tiendabackend.fly.dev/api/articulos/`);
        data = await response.json();
    }

    onMount( getArticulos );

    $: datosFiltrados = data.filter( articulo => RegExp(busqueda, "i").test(articulo.nombre) );
</script>

<Buscar bind:busqueda/>
<hr>

{#each datosFiltrados as  articulo}
    <p>{articulo.nombre}</p>
    <p>{articulo.precio}</p>
    <br>
{/each}