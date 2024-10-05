<template>
  <div class="container">
    <form enctype="multipart/form-data" method="post">
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-person-lines-fill"></i> Datos del Acompañante
            </span>
            <span class="opciones-formulario"></span>
          </p>
        </div>
        <div class="card-body">
          <div class="col-8">
            <div class="mb-3">
              <div class="form-check">
                <input
                  class="form-check-input"
                  type="checkbox"
                  id="sinAcompanante"
                  v-model="sinAcompanante"
                />
                <label class="form-check-label" for="sinAcompanante">
                  <strong>Asiste sin Acompañante</strong>
                </label>
              </div>
            </div>
          </div>
          <hr />
          <div class="row">
            <div class="col-lg-6 col-md-12">
              <div class="mb-3">
                <label for="nombres" class="form-label">
                  <strong class="strong-form">Nombres</strong>
                </label>
                <input
                  id="nombres"
                  class="form-control"
                  type="text"
                  placeholder=""
                  v-model="formData.nombres"
                  :disabled="sinAcompanante"
                  required
                />
              </div>
            </div>
            <div class="col-lg-6 col-md-12">
              <div class="mb-3">
                <label for="apellidos" class="form-label">
                  <strong class="strong-form">Apellidos</strong>
                </label>
                <input
                  id="apellidos"
                  class="form-control"
                  type="text"
                  placeholder=""
                  v-model="formData.apellidos"
                  :disabled="sinAcompanante"
                  required
                />
              </div>
            </div>
            <div class="col-lg-6 col-md-12">
              <div class="mb-3">
                <label for="edad" class="form-label">
                  <strong>Edad</strong>
                </label>
                <input
                  id="edad"
                  class="form-control"
                  type="number"
                  placeholder="0"
                  v-model="formData.edad"
                  :disabled="sinAcompanante"
                  required
                />
              </div>
            </div>
            <div class="col-lg-6 col-md-12">
              <div class="mb-3">
                <label for="celular" class="form-label">
                  <strong>Celular</strong>
                </label>
                <input
                  id="celular"
                  class="form-control"
                  type="tel"
                  placeholder="0"
                  v-model="formData.celular"
                  :disabled="sinAcompanante"
                  required
                />
              </div>
            </div>
            <div class="col-lg-6 col-md-12">
              <div class="mb-3">
                <label for="documento" class="form-label">
                  <strong>Documento</strong>
                </label>
                <input
                  id="documento"
                  class="form-control"
                  type="text"
                  placeholder="0"
                  v-model="formData.documento"
                  :disabled="sinAcompanante"
                  required
                />
              </div>
            </div>
            <div class="col-lg-6 col-md-12">
              <div class="mb-3">
                <label for="parentesco" class="form-label">
                  <strong>Parentesco</strong>
                </label>
                <select
                  id="parentesco"
                  class="form-select"
                  v-model="formData.parentesco"
                  :disabled="sinAcompanante"
                  required
                >
                  <option disabled selected>Seleccione</option>
                  <option
                    v-for="parentesco in parentescos"
                    :key="parentesco.id"
                    :value="parentesco.label"
                  >
                    {{ parentesco.label }}
                  </option>
                </select>
              </div>
            </div>
          </div>
          <!-- Botón para capturar los datos -->
          <div class="mt-3">
            <button
              type="button"
              class="btn btn-custom btn-icon mb-2"
              @click="capturarDatos"
              :disabled="sinAcompanante"
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
import { parentescos } from "../../bd/bd.js";

export default {
  data() {
    return {
      parentescos,
      sinAcompanante: false,
      formData: {
        nombres: "",
        apellidos: "",
        edad: "",
        celular: "",
        documento: "",
        parentesco: "",
      },
    };
  },
  methods: {
    capturarDatos() {
      // Verificamos si algún campo está vacío
      if (
        !this.formData.nombres ||
        !this.formData.apellidos ||
        !this.formData.edad ||
        !this.formData.celular ||
        !this.formData.documento ||
        !this.formData.parentesco
      ) {
        Swal.fire("Por favor, complete todos los campos.");
      } else {
        // Capturamos los datos si están todos completos
        const datosAcompanante = {
          nombres: this.formData.nombres,
          apellidos: this.formData.apellidos,
          edad: this.formData.edad,
          celular: this.formData.celular,
          documento: this.formData.documento,
          parentesco: this.formData.parentesco,
        };

        console.log("Datos del acompañante:", datosAcompanante);
      }
    },
  },
};
</script>
