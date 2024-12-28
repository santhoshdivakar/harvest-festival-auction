<script>
    import {navigate} from 'svelte-routing';
    
</script>

<style>
    main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
    .flex-container {
        display: flex;
        justify-content: space-between;
    }

    .flex-item {
        flex: 1;
        border: 2px solid blue;
        margin: 10px;
        padding: 20px;
        text-align: center;
        height: 20vh; 
        background-color: #e1ebe1;
        color: rgb(97, 3, 3);
        font-size: 2em;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
    }
    .flex-item:hover {
        background-color: #bcf3bf;
    }
    @media (max-width: 600px) {
        .flex-container {
            flex-direction: column;
        }
    }
</style>

<main>
    <h1>Harvest Festival 2024!</h1>
	<p> This season, articipate in the joy of giving</p>
    <div class="flex-container">
        <div class="flex-item" on:click={() => navigate('/newItem')}>New Item</div>
        <div class="flex-item" on:click={() => navigate('/auction')}>Go to Auction</div>
    </div>
    
</main>
