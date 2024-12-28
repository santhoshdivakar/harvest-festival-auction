<script>
  let name = '';
  let description = '';
  let buyingPrice = '';
  let bidPrice = '';
  let photos = [];
  let photoURLs = [];
  async function submitForm(event) {
    // Handle form submission here
    event.preventDefault();
    const formData = new FormData();
    formData.append('name', name);
    formData.append('description', description);
    formData.append('buyingPrice', buyingPrice);
    formData.append('bidPrice', bidPrice);
    formData.append('category', 'test');
    formData.append('userId', 0);
    formData.append('quantity', 1);
    Array.from(photos).forEach((photo, index) => {
      formData.append('photos', photo, `photo${index}`);
    });

    const response = await fetch('/api/newItem', {
      method: 'POST',
      body: formData,
      headers: {
        'Content-Type': 'multipart/form-data',
        'Bearer': 'xxx'//localStorage.getItem('token')
      }
    });
    
    if (response.ok) {
      const item = await response.json();
      console.log(item);
      // Redirect to item page
      window.location = `/item/${item._id}`;
    } else {
      console.log('Error creating item');
      alert('Error creating item', response.statusText);
    }

  };
  $: if (photos && photos.length > 0) {
    photoURLs = Array.from(photos).map(photo => URL.createObjectURL(photo));
  }
</script>

<main>
  <h1>New Item</h1>
  <form on:submit|preventDefault={submitForm}>
    <label>
      Name of item:
      <input type="text" bind:value={name} required />
    </label>
    <label>
      Description:
      <textarea bind:value={description} required></textarea>
    </label>
    <label>
      Buying price:
      <input type="number" bind:value={buyingPrice} required />
    </label>
    <label>
      Bid price:
      <input type="number" bind:value={bidPrice} required />
    </label>
    <label> 
      Photo:
      <input type="file" bind:files={photos} accept="image/*" capture  multiple required />
    </label>
    <button type="submit">Submit</button>
  </form>
  {#each photoURLs as photoURL (photoURL)}
  <img src={photoURL} alt="Selected Photos" class="uploadPhoto"/>
  {/each}
</main>

<style>
  .uploadPhoto {
    width: 25vw;
    max-width: 100;
    height: auto;
    object-fit: contain;
  }

  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
    background-color: #f8f8f8;
  }

  input, textarea {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  button {
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
  }

  button:hover {
    background-color: #0056b3;
  }
  
</style>
