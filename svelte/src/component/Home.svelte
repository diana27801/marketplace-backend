<script>
    const ItemConditions = {
        USED: 'USED',
        GOOD: 'GOOD',
        EXCELLENT: 'EXCELLENT'
    };

    const Categories = {
        CAR: 'CAR',
        CLOTHING_SHOES_AND_ACCESSORIES: 'CLOTHING_SHOES_AND_ACCESSORIES',
        SPORTING_GOODS: 'SPORTING_GOODS',
        HOME_AND_GARDEN: 'HOME_AND_GARDEN',
        TOYS_AND_HOBBIES: 'TOYS_AND_HOBBIES',
        BUSINESS_AND_INDUSTRIAL: 'BUSINESS_AND_INDUSTRIAL',
        HEALTH_AND_BEAUTY: 'HEALTH_AND_BEAUTY',
        PET_SUPPLIES: 'PET_SUPPLIES',
        BABY_ESSENTIALS: 'BABY_ESSENTIALS',
        ELECTRONICS: 'ELECTRONICS',
        COLLECTIBLES_AND_ART: 'COLLECTIBLES_AND_ART',
        BOOKS_MOVIES_AND_MUSIC: 'BOOKS_MOVIES_AND_MUSIC'
    };

    let title = '';
    let category = '';
    let description = '';
    let condition = '';

    async function createAuction() {
        const response = await fetch("http://localhost:8080/auctions", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                "X-Username": "diana"
            },
            body: JSON.stringify({
                title,
                category,
                description,
                condition
            })
        });

        if (response.ok) {
            // Handle successful response
            const data = await response.json();
            console.log('New auction created:', data);
        } else {
            // Handle failed response
            console.error('Failed to create new auction:', response.statusText);
        }
    }
</script>

<form on:submit|preventDefault={createAuction}>
    <div class="container-fluid navigation pb-5 mb-3">
        <div class="card">
        <div class="card-header">
            Erstell ein Angebot
        </div>
        <div class="card-body">
            <div class="form-row">
                <div class="form-group col-md-6">
                    <label for="title">Title:</label>
                    <input type="text" class="form-control" id="title" bind:value={title} required>
                </div>
                <div class="form-group col-md-6">
                    <label for="category">Category:</label>
                    <select class="form-control" id="category" bind:value={category} required>
                        <option value="">Select a category</option>
                        {#each Object.keys(Categories) as cat}
                            <option value={Categories[cat]}>{cat}</option>
                        {/each}
                    </select>
                </div>
            </div>
            <div class="form-row">
                <div class="form-group col-md-6">
                    <label for="condition">Condition:</label>
                    <select class="form-control" id="condition" bind:value={condition} required>
                        <option value="">Select item condition</option>
                        {#each Object.keys(ItemConditions) as cond}
                            <option value={ItemConditions[cond]}>{cond}</option>
                        {/each}
                    </select>
                </div>
                <div class="form-group col-md-6">
                    <label for="description">Description:</label>
                    <textarea class="form-control" id="description" bind:value={description}></textarea>
                </div>
                <div class="form-group col-md-2">
                    <button type="submit">Create Auction</button>
                </div>
            </div>
        </div>
        </div>
    </div>
</form>

<style>
    .card-header{
        background: #badbcc;
    }
    .card {
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
</style>

