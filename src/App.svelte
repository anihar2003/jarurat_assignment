<script>
  import AddService from "./lib/AddService.svelte";
  import ServiceList from "./lib/ServiceList.svelte";
  import UpdateService from "./lib/UpdateService.svelte";

  let service_list = [
    {
      id: 1,
      name: "Blood Test",
      description: "Complete blood test and Analysis",
      price: "500",
    },
    {
      id: 2,
      name: "Complete Body CheckUp",
      description: "Complete Body Checkup and Analysis",
      price: "1000",
    }
  ];

  let serviceToUpdate = null; 
  let errorMessage = '';

  function handleAddService(event) {
    const { name, description, price } = event.detail;
    
    if (!name || !description || !price) {
      errorMessage = 'All fields are required to add a service!';
      return;
    }

    errorMessage = '';
    service_list = [...service_list, event.detail]; 
  }

  function handleDeleteService(id) {
    service_list = service_list.filter(service => service.id !== id); 
  }

  function handleUpdateService(updatedService) {
    if (!updatedService.name || !updatedService.description || !updatedService.price) {
      errorMessage = 'All fields are required to update the service!';
      return;
    }

    errorMessage = '';
    service_list = service_list.map(service =>
      service.id === updatedService.id ? updatedService : service
    );
    serviceToUpdate = null; 
  }

  function openUpdateForm(id) {
    serviceToUpdate = service_list.find(service => service.id === id); 
  }
</script>

<style>
  .container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    font-family: Arial, sans-serif;
  }

  h1 {
    text-align: center;
    color: #333;
  }

  .error-message {
    color: red;
    text-align: center;
    margin: 10px 0;
    font-weight: bold;
  }

  .service-list {
    margin-top: 20px;
  }
</style>

<div class="container">
  <h1>Manage Service</h1>
  <AddService service_list={service_list} on:addService={handleAddService} />
  
  {#if errorMessage}
    <p class="error-message">{errorMessage}</p>
  {/if}

  <div class="service-list">
    <h2>Service List</h2>
    <ServiceList 
      service_list={service_list} 
      onDelete={handleDeleteService}
      onUpdate={openUpdateForm} 
    />
  </div>

  {#if serviceToUpdate}
    <UpdateService service={serviceToUpdate} onUpdate={handleUpdateService} />
  {/if}
</div>
