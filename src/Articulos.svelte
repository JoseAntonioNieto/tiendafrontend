<script>
    import { getContext } from "svelte";
    import { data } from "./store";
    import { onMount } from "svelte";
    import Buscar from "./Buscar.svelte";
    import Articulo from "./Articulo.svelte";
    import Boton from "./Boton.svelte";

    let articuloInsert = {};

    let datosFiltrados = [];
    let busqueda = "";
    const URL = getContext("URL");

    async function getArticulos() {
        const response = await fetch(URL.articulos);
        $data = await response.json();
    }

    onMount( getArticulos );

    

    $: datosFiltrados = $data.filter( articulo => RegExp(busqueda, "i").test(articulo.nombre) );
</script>

<Buscar bind:busqueda/>
<hr>
<Articulo bind:articulo={articuloInsert}/>
<Boton tipo="insertar" documento={articuloInsert}/>
<hr>

{#each datosFiltrados as articulo}
    <!--
    <p>{articulo.nombre}</p>
    <p>{articulo.precio}</p>
    -->
    <Articulo bind:articulo={articulo}/>
    <Boton tipo="modificar" documento={articulo}/>
    <Boton tipo="eliminar" documento={articulo}/>
    <br>
{/each}