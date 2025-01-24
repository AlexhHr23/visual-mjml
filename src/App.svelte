<script>
  import EmailPreview from './lib/components/EmailPreview.svelte'; // Ajusta la ruta si es necesario

  // Datos dinámicos que puedes modificar
  let userName = "Pedro";
  let confirmationLink = "https://miweb.com/confirmar";
</script>

<main>
  <h1>Previsualización del correo</h1>

  <EmailPreview  />

  <div>
    <h2>Actualiza los datos</h2>
    <label>
      Nombre del usuario:
      <input type="text" bind:value={userName} />
    </label>
    <label>
      Enlace de confirmación:
      <input type="text" bind:value={confirmationLink} />
    </label>
  </div>
</main>

<style>
  main {
    font-family: Arial, sans-serif;
    margin: 20px;
  }
  input {
    display: block;
    margin: 10px 0;
    padding: 5px;
    border: 1px solid #ddd;
    border-radius: 4px;
    width: 100%;
    max-width: 400px;
  }
  label {
    margin: 10px 0;
    font-size: 14px;
    display: block;
  }
</style>
