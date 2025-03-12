<script>
    import BotonesAcciones from '$lib/BotonesAcciones.svelte';
    import ModalCancion from '$lib/ModalCancion.svelte';
  
    // Estado de las canciones
    let canciones = [
      { id: 1, titulo: 'Rosa Pastel', artista: 'Belanova', duracion: '3:09' },
      { id: 2, titulo: 'Monster', artista: 'Skillet Awake', duracion: '2:59'},
      { id: 3, titulo: 'ずっと真夜中でいいのに。『シェードの埃は延長』', artista: 'ZUTOMAYO ', duracion: '2:59'},
      { id: 4, titulo: 'No digas nada', artista: 'Latin Mafia', duracion: '3:42' },
      { id: 5, titulo: 'Ella Te Las Va a Pegar', artista: 'Jon Z', duracion: '3:37' }
    ];
  
    // Estado del modal
    let mostrarModal = false;
    let cancionEditando = null;
  
    // Estado de búsqueda
    let busqueda = '';
  
    // Filtrar canciones por título o artista
    const cancionesFiltradas = () => {
      return canciones.filter(
        (cancion) =>
          cancion.titulo.toLowerCase().includes(busqueda.toLowerCase()) ||
          cancion.artista.toLowerCase().includes(busqueda.toLowerCase())
      );
    };
  
    // Funciones del CRUD
    const agregarCancion = (cancion) => {
      canciones = [...canciones, { ...cancion, id: canciones.length + 1 }];
      mostrarModal = false;
    };
  
    const editarCancion = (cancion) => {
      canciones = canciones.map((c) => (c.id === cancion.id ? cancion : c));
      mostrarModal = false;
    };
  
    const eliminarCancion = (id) => {
      canciones = canciones.filter((c) => c.id !== id);
    };
  
    const abrirModal = (cancion = null) => {
      cancionEditando = cancion;
      mostrarModal = true;
    };
  </script>
  
  <h1>Lista de Canciones</h1>
  
  <!-- Input de búsqueda -->
  <input
    class="input-busqueda"
    type="text"
    bind:value={busqueda}
    placeholder="Buscar por título o artista"
  />
  
  <!-- Botón para agregar canción -->
  <button class="boton-agregar" on:click={() => abrirModal()}>Agregar Canción</button>
  
  <!-- Tabla de canciones -->
  <div class="contenedor-tabla">
    <table>
      <thead>
        <tr>
          <th>Título</th>
          <th>Artista</th>
          <th>Duración</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        {#each cancionesFiltradas() as cancion}
          <tr>
            <td>{cancion.titulo}</td>
            <td>{cancion.artista}</td>
            <td>{cancion.duracion}</td>
            <td>
              <!-- Componente BotonesAcciones -->
              <BotonesAcciones
                on:editar={() => abrirModal(cancion)}
                on:eliminar={() => eliminarCancion(cancion.id)}
              />
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
  
  <!-- Modal para agregar/editar canción -->
  {#if mostrarModal}
    <ModalCancion
      {cancionEditando}
      on:guardar={(e) => (cancionEditando ? editarCancion(e.detail) : agregarCancion(e.detail))}
      on:cerrar={() => (mostrarModal = false)}
    />
  {/if}

  
  <style>
    h1 {
      text-align: center;
      font-size: 2.5rem;
      color: #2c3e50;
      margin-bottom: 20px;
    }
  
    .boton-agregar {
      display: block;
      margin: 20px auto;
      padding: 10px 20px;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
      transition: transform 0.5s ease;     }
  
    .boton-agregar:hover {
        transform: rotate(360deg); 
    }
  
    .input-busqueda {
      display: block;
      width: 100%;
      max-width: 400px;
      margin: 20px auto;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      font-size: 1rem;
    }
  
    .contenedor-tabla {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 50vh;
      padding: 20px;
      box-sizing: border-box;
    }
  
    table {
      width: 100%;
      max-width: 800px;
      border-collapse: collapse;
      background: white;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
  
    th,
    td {
      border: 1px solid #ddd;
      padding: 12px;
      text-align: left;
    }
  
    th {
      background-color: #6494bc;
      color: white;
    }
  
    @media (max-width: 768px) {
      th,
      td {
        padding: 8px;
      }
  
      table {
        font-size: 14px;
      }
    }
  
    @media (max-width: 480px) {
      th,
      td {
        padding: 6px;
      }
  
      table {
        font-size: 12px;
      }
    }
  </style>
  