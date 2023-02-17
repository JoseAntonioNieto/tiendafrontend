<script>
    import { onMount } from "svelte";
    import { getContext } from "svelte";
    const URL = getContext("URL");

    export let documento = {};

    export let tipo = "";

    let handler = () => {};

    function insertar() {
        console.log(tipo);
        let opciones = {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento)
        };
        fetch(URL.articulos, opciones)
            .then(res => res.json())
            .then(data => console.log(data))
            .catch();
        console.log(documento.nombre);
    }

    function modificar() {
        console.log(tipo);
        let opciones = {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento)
        };
        fetch(`${URL.articulos}${documento._id}`, opciones)
            .then(res => res.json())
            .then(data => console.log(data))
            .catch();
        console.log(`${documento._id} ${documento.nombre}`);
    }

    function eliminar() {
        let opciones = {
            method: "DELETE",
            headers: { "Content-Type": "application/json" },
        };
        fetch(`${URL.articulos}${documento._id}`, opciones)
            .then(res => res.json())
            .then(data => console.log(data))
            .catch();
    }

    function setUp() {
        if (tipo == "insertar") {
            handler = insertar;
        } else if (tipo == "modificar") {
            handler = modificar;
        } else if (tipo == "eliminar") {
            handler = eliminar;
        }
    };

    onMount(setUp);
</script>
<input type="button" value="{tipo.toUpperCase()}" on:click={handler}>
