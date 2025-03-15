<script>
   
    export let eliminarCancion;
    export let editarCancion;
    
</script>
  
  <style>
    button {
      margin: 0 5px;
      padding: 5px 10px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: transform 0.5s ease; 
    }
  
    button:first-child {
        background-color: #3498db;
        color: white;
    }
  
    button:last-child {
      background-color: #dc3545;
      color: white;
    }
  
    button:hover {
      transform: rotate(360deg); 
    }
  </style>
  
  <button on:click={editarCancion}>Editar</button>
  <button on:click={eliminarCancion}>Eliminar</button>