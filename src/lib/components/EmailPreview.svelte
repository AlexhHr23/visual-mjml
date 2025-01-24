<script>
    const applicationId = "a1dd3caf-2f9f-48ba-a7b5-71a2952d9efe";
    const publicKey = "80fc4ae1-5a8d-4c13-8e30-c780a568dafe";
  
    let mjmlCode = ``;
  

    let renderedHTML = "";
    let error = null;
  
    async function renderMJML() {
      error = null; 
      try {
        const response = await fetch("https://api.mjml.io/v1/render", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Authorization: "Basic " + btoa(`${applicationId}:${publicKey}`), 
          },
          body: JSON.stringify({ mjml: mjmlCode }),
        });
  
        const data = await response.json();
  
        if (response.ok && data.html) {
          renderedHTML = data.html;
        } else {
          error = data.message || "Ocurrió un error al procesar MJML.";
        }
      } catch (err) {
        error = "Error de red: " + err.message;
      }
    }
  

    renderMJML();
  </script>
  
  <div>
    <h2>Edita tu código MJML</h2>
    <textarea bind:value={mjmlCode} rows="10" cols="50" on:input={renderMJML}></textarea>
  </div>
  
  {#if error}
    <div class="error">Error: {error}</div>
  {/if}
  
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
  