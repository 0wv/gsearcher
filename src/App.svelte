<script>
	import { dndzone } from "svelte-dnd-action";
	import { flip } from "svelte/animate";

	let q;

	function appendToSearchHistory(q) {
		localStorage.setItem(
			"searchHistory",
			JSON.stringify([
				...JSON.parse(localStorage.getItem("searchHistory")),
				q,
			])
		);
	}

	function initializeSearchHistory() {
		if (localStorage.getItem("searchHistory") !== null) {
			return;
		}

		localStorage.setItem("searchHistory", JSON.stringify([]));
	}

	function resetClick() {
		q = "";
	}

	function searchClick() {
		if (q === "") {
			return;
		}

		appendToSearchHistory(q);
		window.location.href = `https://google.com/search?q=${q}`;
	}

	initializeSearchHistory();
</script>

<main>
	<input bind:value={q} type="text" />
	<button on:click={searchClick}>検索</button>
	<button on:click={resetClick}>リセット</button>
	<ul>
		{#each JSON.parse(localStorage.getItem("searchHistory")) as q}
			<li>{q}</li>
		{/each}
	</ul>
</main>

<style></style>
