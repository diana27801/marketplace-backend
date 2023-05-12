<script>
    import { onMount } from 'svelte';

    let auctions = [];

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

    onMount(getAuctions);
</script>
<div class="container-fluid navigation pb-5 ">
{#if auctions.length > 0}
    {#each auctions as auction}
        <div class="card mb-3">
            <div class="card-header">
                {auction.title}
            </div>
            <div class="card-body ">
                <p class="card-title">{auction.description}</p>
                <p class="card-text">{auction.category}</p>
                <p class="card-text">{auction.condition}</p>
            </div>
        </div>
    {/each}
{:else}
    <p>No auctions found.</p>
{/if}
</div>

<style>
    button{
        width: 50%;
        float: right;
    }
    .card-header{
        background: #badbcc;
    }
    .card {
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
</style>