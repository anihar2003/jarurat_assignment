<script>
    export let service = {};
    export let onUpdate = () => {};
    let name = service.name;
    let description = service.description;
    let price = service.price;
  
    const handleUpdate = () => {
      if (name && description && price) {
        const updatedService = {
          ...service,
          name,
          description,
          price,
        };
        onUpdate(updatedService);
      } else {
        alert("Please fill in all the fields before submitting!");
      }
    };
</script>

<style>
  .container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background: rgba(0, 0, 0, 0.7);
    z-index: 1000;
  }

  .container_element {
    background: white;
    padding: 20px;
    border-radius: 10px;
    width: 320px;
    text-align: center;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
    transition: transform 0.3s ease-in-out;
  }

  .container_element h3 {
    margin-bottom: 15px;
    color: #333;
  }

  .container_element input {
    width: 100%;
    margin: 10px 0px;
    padding: 5px;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 1rem;
    transition: border-color 0.3s;
  }

  .container_element input:focus {
    border-color: #007BFF;
    outline: none;
  }

  .container_element button {
    margin-top: 10px;
    padding: 10px 20px;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .container_element button:hover {
    background-color: #0056b3;
  }

  .container_element button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
</style>

<div class="container">
  <div class="container_element">
    <h3>Update Service</h3>
    <input type="text" bind:value={name} placeholder="Service Name" required />
    <input type="text" bind:value={description} placeholder="Description" required />
    <input type="number" bind:value={price} placeholder="Price" required />
    <button on:click={handleUpdate} disabled={!name || !description || !price}>Update</button>
  </div>
</div>
