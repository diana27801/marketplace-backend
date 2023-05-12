<script lang="ts">
	import {Route, Router} from "svelte-navigator";
	import Header from "./component/Header.svelte";
	import Footer from "./component/Footer.svelte";
	import AuctionCard from "./component/AuctionCard.svelte";
	import BidCard from "./component/BidCard.svelte";
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

		<Route path="bid">
			<BidCard/>
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