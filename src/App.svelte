<script>
	import { dndzone } from "svelte-dnd-action";
	import { flip } from "svelte/animate";

	let searchQuery;

	function appendToSearchHistory(searchQuery) {
		localStorage.setItem(
			"searchHistory",
			JSON.stringify([
				...JSON.parse(localStorage.getItem("searchHistory")),
				searchQuery,
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
		searchQuery = "";
	}

	function searchClick() {
		if (searchQuery === "") {
			return;
		}

		appendToSearchHistory(searchQuery);
		window.location.href = `https://google.com/search?q=${searchQuery}`;
	}

	initializeSearchHistory();
</script>

<main>
	<input bind:value={searchQuery} type="text" />
	<button on:click={searchClick}>検索</button>
	<button on:click={resetClick}>リセット</button>
	<ul>
		{#each JSON.parse(localStorage.getItem("searchHistory")) as searchQuery}
			<li>{searchQuery}</li>
		{/each}
	</ul>
</main>

<style></style>
