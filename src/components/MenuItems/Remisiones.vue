<template>
  <div class="container">
    <form>
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-send"></i> Remisiones
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
              <!-- Primera fila: Motivo de remisión y Diagnóstico -->
              <div class="row mt-3">
                <div class="col-md-6 mb-3">
                  <label for="motivo-remision" class="form-label"
                    ><strong class="strong-form"
                      >Motivo de la remisión</strong
                    ></label
                  >
                  <textarea
                    class="form-control scrollable-textarea"
                    id="motivo-remision"
                    rows="3"
                    v-model="motivoRemision"
                  ></textarea>
                </div>
                <div class="col-md-6 mb-3">
                  <label for="diagnostico-consulta" class="form-label"
                    ><strong class="strong-form"
                      >Diagnóstico de la consulta</strong
                    ></label
                  >
                  <textarea
                    class="form-control scrollable-textarea"
                    id="diagnostico-consulta"
                    rows="3"
                    v-model="diagnosticoConsulta"
                    readonly
                  ></textarea>
                </div>
              </div>

              <!-- Segunda fila: Tipo de servicio y Análisis -->
              <div class="row mt-3">
                <div class="col-md-6 mb-3">
                  <!-- Grupo de clasificación y especificación del servicio -->
                  <div class="mb-2">
                    <label for="clasificacion-servicio" class="form-label">
                      <strong>Clasificación Servicio</strong>
                    </label>
                    <select
                      class="form-select mb-4"
                      id="clasificacion-servicio"
                      v-model="clasificacionServicio"
                    >
                      <option value="" disabled>Seleccione una opción</option>
                      <option
                        v-for="opcion in clasificacionesServicio"
                        :key="opcion.id"
                        :value="opcion.id"
                      >
                        {{ opcion.label }}
                      </option>
                    </select>
                  </div>

                  <div>
                    <label for="especificacion-servicio" class="form-label">
                      <strong>Especificación del servicio</strong>
                    </label>
                    <select
                      class="form-select"
                      id="especificacion-servicio"
                      v-model="especificacionServicio"
                    >
                      <option value="" disabled>Seleccione una opción</option>
                      <option
                        v-for="opcion in especificacionesServicio"
                        :key="opcion.id"
                        :value="opcion.id"
                      >
                        {{ opcion.label }}
                      </option>
                    </select>
                  </div>
                </div>

                <div class="col-md-6 mb-3">
                  <label for="analisis-consulta" class="form-label"
                    ><strong>Análisis de la consulta</strong></label
                  >
                  <textarea
                    class="form-control scrollable-textarea2"
                    id="analisis-consulta"
                    rows="3"
                    v-model="analisisConsulta"
                    readonly
                  ></textarea>
                </div>
              </div>

              <hr />

              <!-- Tercera fila: Plan de manejo -->
              <div class="row mt-3">
                <div class="col-12 mb-3">
                  <label for="plan-manejo" class="form-label"
                    ><strong>Plan de manejo</strong></label
                  >
                  <textarea
                    class="form-control scrollable-textarea"
                    id="plan-manejo"
                    rows="3"
                    v-model="planManejo"
                    readonly
                  ></textarea>
                </div>
              </div>

              <!-- Cuarta fila: Observaciones de la remisión -->
              <div class="row mt-3">
                <div class="col-12 mb-3">
                  <label for="observaciones-remision" class="form-label"
                    ><strong>Observaciones de la remisión</strong></label
                  >
                  <textarea
                    class="form-control scrollable-textarea"
                    id="observaciones-remision"
                    rows="3"
                    v-model="observacionesRemision"
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

            <div
              class="tab-pane fade"
              id="profile-tab-pane"
              role="tabpanel"
              aria-labelledby="profile-tab"
              tabindex="0"
            >
              <!-- DataTable -->
              <div class="container my-4">
                <div class="row">
                  <div class="col-sm-12 col-md-12 col-lg-12 col-xl-12">
                    <div class="table-responsive">
                      <!-- Agregar contenedor para el scroll -->
                      <table ref="dataTable" class="table table-striped">
                        <thead>
                          <tr>
                            <th class="centered">#</th>
                            <th class="centered">Name</th>
                            <th class="centered">Email</th>
                            <th class="centered">City</th>
                            <th class="centered">Company</th>
                            <th class="centered">Status</th>
                            <th class="centered">Options</th>
                          </tr>
                        </thead>
                        <tbody></tbody>
                      </table>
                    </div>
                    <!-- Cierre del contenedor -->
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
import { ref, onMounted } from "vue";
import $ from "jquery";
import "datatables.net";
import "datatables.net-dt/css/dataTables.dataTables.css";

import {
  clasificacionesServicio,
  especificacionesServicio,
} from "../../bd/bd.js";

export default {
  setup() {
    const motivoRemision = ref("");
    const diagnosticoConsulta = ref(
      "aquí va el diagnóstico primario seleccionado en la ventana de diagnóstico."
    );
    const clasificacionServicio = ref("");
    const especificacionServicio = ref("");
    const analisisConsulta = ref(
      "aquí va el análisis de la consulta consignado en la pestaña análisis."
    );
    const planManejo = ref(
      "aquí va el análisis de la consulta consignado en la pestaña análisis."
    );
    const observacionesRemision = ref("");

    const dataTable = ref(null);

    const capturarDatos = () => {
      if (
        !motivoRemision.value.trim() ||
        !clasificacionServicio.value ||
        !especificacionServicio.value ||
        !observacionesRemision.value.trim()
      ) {
        alert("Por favor, complete todos los campos obligatorios.");
        return;
      }

      const datosRemision = {
        motivoRemision: motivoRemision.value,
        diagnosticoConsulta: diagnosticoConsulta.value,
        clasificacionServicio: clasificacionServicio.value,
        especificacionServicio: especificacionServicio.value,
        analisisConsulta: analisisConsulta.value,
        planManejo: planManejo.value,
        observacionesRemision: observacionesRemision.value,
      };

      console.log("Datos de la remisión:", datosRemision);
    };

    // Data Table ignorar por ahora
    const dataTableOptions = {
      lengthMenu: [5, 10, 15, 20, 100, 200, 500],
      columnDefs: [
        { className: "centered", targets: [0, 1, 2, 3, 4, 5, 6] },
        { orderable: false, targets: [5, 6] },
        { searchable: false, targets: [1] },
      ],
      pageLength: 3,
      destroy: true,
      language: {
        lengthMenu: "Mostrar _MENU_ registros por página",
        zeroRecords: "Ningún usuario encontrado",
        info: "Mostrando de _START_ a _END_ de un total de _TOTAL_ registros",
        infoEmpty: "Ningún usuario encontrado",
        infoFiltered: "(filtrados desde _MAX_ registros totales)",
        search: "Buscar:",
        loadingRecords: "Cargando...",
        paginate: {
          first: "Primero",
          last: "Último",
          next: "Siguiente",
          previous: "Anterior",
        },
      },
    };

    const initDataTable = async () => {
      if ($.fn.DataTable.isDataTable(dataTable.value)) {
        $(dataTable.value).DataTable().destroy();
      }

      await listUsers();

      $(dataTable.value).DataTable(dataTableOptions);
    };

    const listUsers = async () => {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );
        const users = await response.json();

        let content = "";
        users.forEach((user, index) => {
          content += `
                  <tr>
                    <td>${index + 1}</td>
                    <td>${user.name}</td>
                    <td>${user.email}</td>
                    <td>${user.address.city}</td>
                    <td>${user.company.name}</td>
                    <td><i class="fa-solid fa-check" style="color: green;"></i></td>
                    <td>
                      <button class="custom-btn custom-edit-btn"><i class="fa-solid fa-pencil"></i></button>
                      <button class="custom-btn custom-delete-btn"><i class="fa-solid fa-trash-can"></i></button>
                    </td>
                  </tr>`;
        });
        $(dataTable.value).find("tbody").html(content);
      } catch (ex) {
        alert(ex);
      }
    };

    onMounted(async () => {
      await initDataTable();
    });

    return {
      motivoRemision,
      diagnosticoConsulta,
      clasificacionServicio,
      especificacionServicio,
      analisisConsulta,
      planManejo,
      observacionesRemision,
      dataTable,
      capturarDatos,

      clasificacionesServicio,
      especificacionesServicio,
    };
  },
};
</script>
