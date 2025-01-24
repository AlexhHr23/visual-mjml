<script>
    // Claves de la API de MJML (sustitúyelas con tus credenciales)
    const applicationId = "a1dd3caf-2f9f-48ba-a7b5-71a2952d9efe";
    const secretKey = "80fc4ae1-5a8d-4c13-8e30-c780a568dafe";
  
    // Código MJML editable
    let mjmlCode = `
      <mjml>
        <mj-body>
          <mj-container>
            <mj-section>
              <mj-column>
                <mj-text align="center" font-size="20px" color="#333">
                  ¡Bienvenido a nuestra plataforma!
                </mj-text>
              </mj-column>
            </mj-section>
            <mj-section>
              <mj-column>
                <mj-text>
                  Hola <b>Usuario</b>,<br><br>
                  Gracias por registrarte. Por favor, confirma tu cuenta haciendo clic en el siguiente botón:
                </mj-text>
                <mj-button href="https://example.com/confirmar" background-color="#007bff" color="white">
                  Confirmar cuenta
                </mj-button>
              </mj-column>
            </mj-section>
            <mj-section>
              <mj-column>
                <mj-text>
                  Si tienes alguna duda, no dudes en contactarnos.<br><br>
                  Saludos,<br>El equipo de Ejemplo
                </mj-text>
              </mj-column>
            </mj-section>
          </mj-container>
        </mj-body>
      </mjml>
    `;
  
    // HTML renderizado
    let renderedHTML = "";
    let error = null;
  
    // Función para llamar al endpoint de MJML
    async function renderMJML() {
      error = null; // Reiniciar error
      try {
        const response = await fetch("https://api.mjml.io/v1/render", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Authorization: "Basic " + btoa(`${applicationId}:${secretKey}`), // Autenticación básica
          },
          body: JSON.stringify({ mjml: mjmlCode }), // Enviar el código MJML
        });
  
        const data = await response.json();
  
        if (response.ok && data.html) {
          renderedHTML = data.html; // Actualizar el HTML renderizado
        } else {
          error = data.message || "Ocurrió un error al procesar MJML.";
        }
      } catch (err) {
        error = "Error de red: " + err.message;
      }
    }
  
    // Llamar a renderMJML al cargar el componente
    renderMJML();
  </script>
  
  <!-- Textarea para editar el código MJML -->
  <div>
    <h2>Edita tu código MJML</h2>
    <textarea bind:value={mjmlCode} rows="10" cols="50" on:input={renderMJML}></textarea>
  </div>
  
  <!-- Mensaje de error si ocurre algún problema -->
  {#if error}
    <div class="error">Error: {error}</div>
  {/if}
  
  <!-- Renderización dinámica del HTML generado -->
  <div class="email-preview">
    {@html renderedHTML}
  </div>
  
  <style>
    .email-preview {
      border: 1px solid #ddd;
      padding: 20px;
      max-width: 600px;
      margin: 20px auto;
      background-color: #fff;
      font-family: Arial, sans-serif;
      line-height: 1.5;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }
  
    textarea {
      width: 100%;
      max-width: 600px;
      margin: 20px auto;
      display: block;
      font-family: monospace;
      font-size: 14px;
      padding: 10px;
    }
  
    .error {
      color: red;
      font-weight: bold;
      margin: 10px 0;
    }
  </style>
  