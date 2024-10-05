<template>
  <div class="container">
    <form enctype="multipart/form-data" method="post">
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-card-checklist"></i> Recomendaciones
            </span>
            <span class="opciones-formulario"></span>
          </p>
        </div>
        <div class="card-body">
          <div class="row">
            <div class="col-12">
              <div class="mb-3">
                <label for="observaciones" class="form-label">
                  <strong
                    >Recomendaciones al paciente relacionadas con la
                    consulta</strong
                  >
                </label>
                <textarea
                  id="observaciones"
                  class="form-control"
                  rows="3"
                  v-model="formData.observaciones"
                ></textarea>
              </div>
            </div>
          </div>
          <!-- Botón para capturar los datos -->
          <div class="mt-3">
            <button
              type="button"
              class="btn btn-custom btn-icon mb-2"
              @click="capturarDatos"
            >
              Guardar
            </button>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        observaciones: "",
      },
      observacionesArray: [],
    };
  },
  methods: {
    capturarDatos() {
      // Verificamos si el campo de observaciones está vacío
      if (this.formData.observaciones.trim() === "") {
        alert("Por favor, complete el campo de observaciones.");
      } else {
        // Dividimos el contenido del textarea en líneas y lo almacenamos en el array
        this.observacionesArray = this.formData.observaciones.split("\n");
        console.log("Array de Observaciones:", this.observacionesArray);
      }
    },
  },
};
</script>
