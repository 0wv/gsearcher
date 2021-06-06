<script>
	import { dndzone } from "svelte-dnd-action";
	import { flip } from "svelte/animate";

	let searchHistory;
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

	function resetHistoryClick() {
		localStorage.removeItem("searchHistory");
		initializeSearchHistory();
		updateSearchHistory();
	}

	function searchClick() {
		if (searchQuery === "") {
			return;
		}

		appendToSearchHistory(searchQuery);
		window.location.href = `https://google.com/search?q=${searchQuery}`;
	}

	function updateSearchHistory() {
		searchHistory = JSON.parse(localStorage.getItem("searchHistory"));
	}

	initializeSearchHistory();
	updateSearchHistory();
</script>

<main>
	<input bind:value={searchQuery} type="text" />
	<button on:click={searchClick}>検索</button>
	<button on:click={resetClick}>リセット</button>
	<button on:click={resetHistoryClick}>履歴をリセット</button>
	<ul>
		{#each searchHistory as searchQuery}
			<li>{searchQuery}</li>
		{/each}
	</ul>
</main>

<style></style>
