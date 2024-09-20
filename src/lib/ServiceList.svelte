<script>
    export let service_list;
    export let onDelete;
    export let onUpdate;
  </script>
  
  <style>
    /* General styles for the list */
    ul {
      list-style: none;
      padding: 0;
      margin: 0;
      display: flex;
      flex-direction: column;
      gap: 15px;
    }
  
    li {
      background: #f9f9f9;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      padding: 20px;
      transition: transform 0.2s;
    }
  
    li:hover {
      transform: translateY(-2px);
    }
  
    p {
      margin: 5px 0;
      font-size: 1rem;
    }
  
    .price {
      font-weight: bold;
      color: #4CAF50;
    }
  
    button {
      background-color: #007BFF;
      color: white;
      border: none;
      border-radius: 5px;
      padding: 10px 15px;
      cursor: pointer;
      transition: background-color 0.3s;
      margin-right: 5px;
    }
  
    button:hover {
      background-color: #0056b3;
    }
  
    button:disabled {
      background-color: #ccc;
      cursor: not-allowed;
    }
  
    .no-services {
      text-align: center;
      font-size: 1.2rem;
      color: #777;
    }
  </style>
  
  <div>
    <ul>
      {#each service_list as { id, name, description, price }, i}
        <li>
          <p><strong>Name:</strong> {name}</p>
          <p><strong>Description:</strong> {description}</p>
          <p class="price">Price: ₹{price}</p>
          <button on:click={() => onDelete(id)}>Delete</button>
          <button on:click={() => onUpdate(id)}>Update</button>
        </li>
      {:else}
        <li class="no-services">No Services Found</li>
      {/each}
    </ul>
  </div>
  