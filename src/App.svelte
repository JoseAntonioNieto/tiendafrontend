<script>
	import Nav from "./Nav.svelte";
	import { Router } from "svelte-routing";
    import Contenido from "./Contenido.svelte";
</script>

<Router>
	<Nav/>
	<Contenido/>
</Router>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
	}

	:global(*) {
		margin: 0;
		padding: 0;
	}
</style>