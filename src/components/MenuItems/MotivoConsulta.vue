<template>
  <div class="container">
    <form>
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-clipboard-pulse"></i> Motivo de Consulta
            </span>
            <span class="opciones-formulario"></span>
          </p>
        </div>

        <div class="card-body">
          <ul class="nav nav-tabs" id="myTab" role="tablist">
            <li class="nav-item" role="presentation">
              <button
                class="nav-link active"
                id="home-tab"
                data-bs-toggle="tab"
                data-bs-target="#home-tab-pane"
                type="button"
                role="tab"
                aria-controls="home-tab-pane"
                aria-selected="true"
              >
                Actual
              </button>
            </li>
            <li class="nav-item" role="presentation">
              <button
                class="nav-link"
                id="profile-tab"
                data-bs-toggle="tab"
                data-bs-target="#profile-tab-pane"
                type="button"
                role="tab"
                aria-controls="profile-tab-pane"
                aria-selected="false"
              >
                Historial
              </button>
            </li>
          </ul>
          <div class="tab-content" id="myTabContent">
            <div
              class="tab-pane fade show active"
              id="home-tab-pane"
              role="tabpanel"
              aria-labelledby="home-tab"
              tabindex="0"
            >
              <div class="row mt-3">
                <!-- Textarea - Motivo Consulta -->
                <div class="col-lg-6 col-md-12">
                  <div class="mb-3">
                    <label for="motivo-consulta" class="form-label"
                      ><strong>Motivo Consulta</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="motivo-consulta"
                      v-model="formData.motivoConsulta"
                      rows="3"
                    ></textarea>
                  </div>
                </div>
                <!-- Input - Dias Evolución -->
                <div class="col-lg-6 col-md-12">
                  <div class="mb-3">
                    <label for="dias-evolucion" class="form-label"
                      ><strong>Días Evolución</strong></label
                    >
                    <input
                      type="number"
                      class="form-control"
                      id="dias-evolucion"
                      v-model="formData.diasEvolucion"
                      placeholder="0"
                    />
                  </div>
                </div>
                <!-- Textarea - Enfermedad Actual -->
                <div class="col-lg-6 col-md-12">
                  <div class="mb-3">
                    <label for="enfermedad-actual" class="form-label"
                      ><strong>Enfermedad Actual</strong></label
                    >
                    <textarea
                      class="form-control scrollable-textarea"
                      id="enfermedad-actual"
                      v-model="formData.enfermedadActual"
                      rows="3"
                    ></textarea>
                  </div>
                </div>
                <!-- Select - Llegada de paciente -->
                <div class="col-lg-6 col-md-12">
                  <div class="mb-3">
                    <label for="llegada-paciente" class="form-label"
                      ><strong>Llegada de paciente</strong></label
                    >
                    <select
                      class="form-select"
                      id="llegada-paciente"
                      v-model="formData.llegadaPaciente"
                      required
                    >
                      <option disabled selected>Seleccione</option>
                      <option
                        v-for="medio in mediosllegada"
                        :key="medio.id"
                        :value="medio.id"
                      >
                        {{ medio.label }}
                      </option>
                    </select>
                  </div>
                </div>
                <!-- Select - Escala de dolor -->
                <div class="col-lg-6 col-md-12">
                  <div class="mb-3">
                    <label for="escala-dolor" class="form-label"
                      ><strong>Escala de dolor</strong></label
                    >
                    <select
                      class="form-select"
                      id="escala-dolor"
                      v-model="formData.escalaDolor"
                      required
                    >
                      <option disabled selected>Seleccione</option>
                      <option
                        v-for="dolor in esdolor"
                        :key="dolor.id"
                        :value="dolor.id"
                      >
                        {{ dolor.label }}
                      </option>
                    </select>
                  </div>
                </div>
                <!-- Select - ¿Es Gestante? -->
                <div class="col-lg-6 col-md-12">
                  <div class="mb-3">
                    <label for="es-gestante" class="form-label"
                      ><strong>¿Es Gestante?</strong></label
                    >
                    <select
                      class="form-select"
                      id="es-gestante"
                      v-model="formData.esGestante"
                      required
                    >
                      <option disabled selected>Seleccione</option>
                      <option
                        v-for="opcion in gestante"
                        :key="opcion.id"
                        :value="opcion.id"
                      >
                        {{ opcion.label }}
                      </option>
                    </select>
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
            <div
              class="tab-pane fade"
              id="profile-tab-pane"
              role="tabpanel"
              aria-labelledby="profile-tab"
              tabindex="0"
            >
              <!-- DataTable -->
              <div class="container">
                <div class="row">
                  <div class="col-lg-12">
                    <div class="table-responsive">
                      <table
                        id="miTabla"
                        class="table table-striped table-bordered"
                        style="width: 100%"
                      >
                        <thead>
                          <tr>
                            <th>Fecha</th>
                            <th>Tipo/Especificación</th>
                            <th>Escala Dolor</th>
                            <th>Motivo Consulta</th>
                            <th>Opciones</th>
                          </tr>
                        </thead>
                        <tbody></tbody>
                      </table>
                    </div>
                  </div>
                </div>
              </div>
              <!-- Data Table -->
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { mediosllegada, esdolor, gestante } from "../../bd/bd.js";

import { onMounted } from "vue";
import $ from "jquery";
import "datatables.net";
import "datatables.net-dt/css/dataTables.dataTables.css";

export default {
  setup() {
    onMounted(() => {
      $("#miTabla").DataTable({
        paging: true, // Activar paginación
        searching: true, // Activar búsqueda
        ordering: true, // Activar ordenamiento por columnas
        pageLength: 10, // Número de filas por página
      });
    });
  },
  data() {
    return {
      mediosllegada,
      esdolor,
      gestante,
      formData: {
        motivoConsulta: "",
        diasEvolucion: "",
        enfermedadActual: "",
        llegadaPaciente: "",
        escalaDolor: "",
        esGestante: "",
      },
    };
  },
  methods: {
    capturarDatos() {
      // Verificar si los campos están vacíos
      if (
        !this.formData.motivoConsulta ||
        !this.formData.diasEvolucion ||
        !this.formData.enfermedadActual ||
        !this.formData.llegadaPaciente ||
        !this.formData.escalaDolor ||
        !this.formData.esGestante
      ) {
        alert("Por favor, complete todos los campos antes de continuar.");
        return;
      }

      const datosCapturados = {
        motivoConsulta: this.formData.motivoConsulta,
        diasEvolucion: this.formData.diasEvolucion,
        enfermedadActual: this.formData.enfermedadActual,
        llegadaPaciente: this.formData.llegadaPaciente,
        escalaDolor: this.formData.escalaDolor,
        esGestante: this.formData.esGestante,
      };

      console.log("Datos capturados:", datosCapturados);
    },
  },
};
</script>
