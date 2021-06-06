<script>
	import { dndzone } from "svelte-dnd-action";
	import { flip } from "svelte/animate";

	let q;

	function resetClick() {
		q = "";
	}

	function searchClick() {
		if (q === "") {
			return;
		}

		window.location.href = `https://google.com/search?q=${q}`;
	}
</script>

<main>
	<input bind:value={q} type="text" />
	<button on:click={searchClick}>検索</button>
	<button on:click={resetClick}>リセット</button>
</main>

<style></style>
