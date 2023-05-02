<script lang="ts">
	import {Route, Router} from "svelte-navigator";
	import Header from "./component/Header.svelte";
	import Footer from "./component/Footer.svelte";
	import AuctionCard from "./component/AuctionCard.svelte";
	import Home from "./component/Home.svelte";
</script>

<Router>
	<main>
		<Header/>
		<Route path="/">
			<Home/>
		</Route>
		<Route path="auction">
			<AuctionCard/>
		</Route>
		<Footer/>
	</main>
</Router>

<style>
	main {
		max-width: 50rem;
		margin: auto;
	}
</style>