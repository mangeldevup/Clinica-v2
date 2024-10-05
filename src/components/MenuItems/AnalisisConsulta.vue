<template>
  <div class="container">
    <form enctype="multipart/form-data" method="post">
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-graph-up"></i> Análisis de la Consulta
            </span>
            <span class="opciones-formulario"></span>
          </p>
        </div>
        <div class="card-body">
          <div class="row">
            <div
              class="col-md-6 mb-3"
              v-for="campo in camposAnalisisConsulta"
              :key="campo.id"
            >
              <label :for="campo.id" class="form-label">
                <strong>{{ campo.label }}</strong>
              </label>
              <textarea
                :id="campo.id"
                class="form-control"
                rows="3"
                v-model="formData[campo.id]"
                :placeholder="campo.placeholder"
              ></textarea>
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
      camposAnalisisConsulta: [
        {
          id: "descripcionAnalisis",
          label: "Descripción y Análisis Médico de la Consulta",
          placeholder: "Ingrese la descripción y análisis médico",
        },
        {
          id: "planManejo",
          label: "Plan de Manejo",
          placeholder: "Ingrese el plan de manejo",
        },
      ],
      formData: {
        descripcionAnalisis: "",
        planManejo: "",
      },
    };
  },
  methods: {
    capturarDatos() {
      // Verificamos si algún campo está vacío
      const camposVacios = Object.entries(this.formData).filter(
        ([key, value]) => value.trim() === ""
      );

      if (camposVacios.length > 0) {
        alert("Por favor, complete todos los campos.");
      } else {
        // Capturamos los datos si están todos completos
        const datosAnalisisConsulta = { ...this.formData };
        console.log(
          "Datos del Análisis de la Consulta:",
          datosAnalisisConsulta
        );
      }
    },
  },
};
</script>
