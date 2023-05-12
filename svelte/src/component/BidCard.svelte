<script>
    import { onMount } from 'svelte';

    let auctions = [];
    let bids = [];
    let bidNumber = 9999;

    async function getAuctions() {
        const url = 'http://localhost:8080/auctions'; // Replace with your actual API endpoint URL

        const response = await fetch(url);

        if (response.ok) {
            const data = await response.json();
            auctions = data.content;
        } else {
            console.error('Failed to fetch auctions: ' + response.statusText);
        }
    }

    async function getAuction(i) {
        const url = `http://localhost:8080/auctions?id=${i}`; // Replace with your actual API endpoint URL
        let auction = "";
        const response = await fetch(url);

        if (response.ok) {
            const data = await response.json();
            return data.content;
        } else {
            console.error('Failed to fetch singel auction: ' + response.statusText);
        }
        return auction;
    }

    async function getBids() {
        let bidNumberString = bidNumber.toString();
        /*bidNumberString = "3"*/
        const url = `http://localhost:8080/bids?auctionIdEq=${bidNumberString}`; // Replace with your actual API endpoint URL
        console.log(url);
        const response = await fetch(url);

        if (response.ok) {
            const data = await response.json();
            bids = data.content;
        } else {
            console.error('Failed to fetch bids: ' + response.statusText);
        }
        console.log(bids);
    }



    async function addBid() {

        const response = await fetch("http://localhost:8080/bids", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                "X-Username": "diana"
            },
            body: JSON.stringify({
                price,
                auctionId
            })
        });

        if (response.ok) {
            // Handle successful response
            const data = await response.json();
            console.log('New bid created:', data);
        } else {
            // Handle failed response
            console.error('Failed to create new bid:', response.statusText);
        }
    }

    let auctionId = 99999;
    let price = '';

    onMount(getAuctions);
    onMount(getBids);
    /*onMount(getBidsAuctions);*/
</script>

<div class="container-fluid navigation pb-5 ">

    {#if auctions.length > 0}
        <!--<p>{auctions[0].id}</p>-->
        <form on:submit|preventDefault={addBid}>
        <div class="card mb-3">
            <div class="card-header">
                Gebot abgeben
            </div>
            <div class="card-body ">
            <label for="auction">Produktnummer für Gebot auswählen:</label>
            <select class="form-control" id="auction" bind:value={auctionId} required>
                <option value="">Select a product</option>
                {#each auctions as auction, index}
                    <option value={index + 1}>{auction.id} - {auction.title}</option>
                {/each}
            </select>

            <div class="form-group col-md-6">
                <label for="price">Höhe des Gebots eingeben:</label>
                <input type="text" class="form-control" id="price" bind:value={price} required>
            </div>

            <div class="form-group col-md-2">
                <button type="submit">Gebot Abgeben</button>
            </div>
            </div>
        </div>
        </form>

    {:else}
    <p>No bids found.</p>
    {/if}


    <form on:submit|preventDefault={getBids}>
    <div class="card mb-3">
        <div class="card-header">Abgegebene Gebote anzeigen</div>
        <div class="card-body ">
        <label for="auction">Auktion auswählen:</label>
        <select class="form-control" id="auction" bind:value={bidNumber} required>
            <option value="">Select a product</option>
            {#each auctions as auction, index}
                <option value={index + 1}>{auction.id} - {auction.title}</option>
            {/each}
        </select>

        <div class="form-group col-md-2">
            <button type="submit">Gebote Anzeigen</button>
        </div>
        </div>
    </div>
    </form>


    <h2>Gebote auf ausgewählte Auktion</h2>



    {#if bids.length > 0}
        {#each bids as bid}
            <div class="card mb-3">
                <div class="card-header">
                    Gebot am: {bid.updatedAt}
                </div>
                <div class="card-body ">
                    <p class="card-title">{bid.price} €</p>
                    <p class="card-title">{bid.username}</p>
                </div>
            </div>
        {/each}
    {:else}
        <p>No bids found.</p>
    {/if}



</div>

<style>
    .card-header{
        background: #badbcc;
    }
    .card {
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
</style>