<script>
    import { createEventDispatcher } from "svelte";
    
    export let service_list = [];
    let name = "";
    let description = "";
    let price = "";
    
    const dispatch = createEventDispatcher();
    
    const AddService = () => {
      const lastId = service_list.length > 0 ? Math.max(...service_list.map(service => service.id)) : 0;
      const newService = {
        id: lastId + 1, 
        name,
        description,
        price,
      };
      dispatch('addService', newService);
      name = "";
      description = "";
      price = ""; 
    };
</script>

<style>
  .form-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    background: #fff;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    padding: 20px;
    width: 300px;
    margin: 20px auto; /* Center the form */
  }

  input {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 1rem;
    transition: border-color 0.3s;
  }

  input:focus {
    border-color: #007BFF;
    outline: none;
  }

  button {
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 10px 15px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  button:hover {
    background-color: #0056b3;
  }

  button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
</style>

<div class="form-container">
    <h3>Add Service</h3>
    <input type="text" bind:value={name} placeholder="Service Name" required />
    <input type="text" bind:value={description} placeholder="Description" required />
    <input type="number" bind:value={price} placeholder="Price" required />
    <button on:click={AddService}>Add Service</button>
</div>
