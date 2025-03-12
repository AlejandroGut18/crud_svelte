<script>
    export let cancionEditando;
  
    let titulo = cancionEditando?.titulo;
    let artista = cancionEditando?.artista || 'Desconocido';
    let duracion = cancionEditando?.duracion || 0;
  
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
  
    const guardar = () => {
      const cancion = { id: cancionEditando?.id, titulo, artista, duracion };
      dispatch('guardar', cancion);
    }
  </script>
  
  <div class="modal">
    <h2>{cancionEditando ? 'Editar Canción' : 'Agregar Canción'}</h2>
    <input type="text" bind:value={titulo} placeholder="Título" />
    <input type="text" bind:value={artista} placeholder="Artista"/>
    <input type="text" bind:value={duracion} placeholder="Duración"/>
    <button on:click={guardar}>Guardar</button>
    <button on:click={() => dispatch('cerrar')}>Cerrar</button>
  </div>

  <style>
    .modal {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
  
    .modal input {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 8px;
      border: 1px solid #ddd;
      border-radius: 5px;
    }
  
    .modal button {
      margin: 5px;
    }
  </style>