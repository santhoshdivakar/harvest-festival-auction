<script>
  import {onMount} from 'svelte';

  let items = [];

  onMount(async () => {
     // Fetch the list of items from the server
    const response = await fetch('/api/items',{
      headers: {
        'Bearer': 'xxx'//localStorage.getItem('token')
      },
      method: 'GET'
    });
    items = await response.json();
    // and store them in the `items` variable
  });
  async function deleteItem(itemId) {
    const response = await fetch(`/api/items/${itemId}`, { method: 'DELETE' });
    if (response.ok) {
      items = items.filter(item => item.id !== itemId);
    }
  }

</script>

<main>
  <h1>Auction</h1>

  {#each  items as  item (item.id)}
    <div class="item-box">
      <div>
        <h2>{item.name}</h2>
        <p>{item.description}</p>
        <p>Current bid: {item.currentBid}</p>
        <p>Buy now price: {item.buyingPrice}</p>      
      </div>
      <div class="delete-icon" on:click={() => deleteItem(item.id)}>&#x1F5D1;</div>
    </div>
  {/each}
</main>

<style>
  .delete-icon {
    cursor: pointer;
  }
</style>
