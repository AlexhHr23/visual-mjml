<script>
  import EmailPreview from './lib/components/EmailPreview.svelte'; // Ajusta la ruta si es necesario

  // Datos dinámicos que puedes modificar
  let userName = "Pedro";
  let confirmationLink = "https://miweb.com/confirmar";
</script>

<main>
  <h1>Previsualización del correo</h1>

  <EmailPreview  />

</main>

<style>
  main {
    font-family: Arial, sans-serif;
    margin: 20px;
  }
</style>
