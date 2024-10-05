<template>
  <!-- Modal para búsqueda de motivo -->
  <div
    class="modal fade"
    id="modalBusquedaMotivo"
    tabindex="-1"
    aria-labelledby="modalBusquedaMotivoLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content">
        <div id="headerm-general" class="modal-header">
          <h5 class="modal-title" id="modalBusquedaMotivoLabel">
            Buscar Motivo de Incapacidad
          </h5>
          <button
            type="button"
            id="closem-general"
            class="close-modal bi bi-x ms-auto"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div id="contenidom-general" class="modal-body">
          <input
            type="text"
            class="form-control mb-3"
            placeholder="Buscar motivo..."
          />
          <ul class="list-group">
            <li
              class="list-group-item"
              @click="
                seleccionarMotivo({ codigo: 'M001', descripcion: 'Motivo 1' })
              "
            >
              Motivo 1
            </li>
            <li
              class="list-group-item"
              @click="
                seleccionarMotivo({ codigo: 'M002', descripcion: 'Motivo 2' })
              "
            >
              Motivo 2
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
  <div class="container">
    <form>
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-calendar-x"></i> Incapacidad Médica
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
                <!-- Motivo de Incapacidad médica -->
                <div class="col-md-6 mb-3">
                  <label for="motivo-incapacidad" class="form-label"
                    ><strong>Motivo de Incapacidad médica</strong></label
                  >
                  <div class="input-group">
                    <input
                      type="text"
                      class="form-control"
                      id="motivo-incapacidad"
                      v-model="motivoIncapacidad"
                      readonly
                    />
                    <button
                      class="btn btn-custom btn-icon"
                      type="button"
                      @click="buscarMotivo"
                    >
                      Buscar
                    </button>
                  </div>
                  <textarea
                    class="form-control mt-2"
                    rows="3"
                    v-model="descripcionMotivo"
                    readonly
                  ></textarea>
                </div>

                <!-- Diagnóstico de la consulta -->
                <div class="col-md-6 mb-3">
                  <label for="diagnostico-consulta" class="form-label"
                    ><strong>Diagnóstico de la consulta</strong></label
                  >
                  <textarea
                    class="form-control"
                    id="diagnostico-consulta"
                    rows="6"
                    v-model="diagnosticoConsulta"
                    readonly
                  ></textarea>
                </div>
              </div>

              <div class="row mt-3">
                <!-- Días de incapacidad médica -->
                <div class="col-md-6 mb-3">
                  <div class="mb-2">
                    <label for="dias-recomendados" class="form-label"
                      ><strong>Días Recomendados:</strong></label
                    >
                    <input
                      type="number"
                      class="form-control"
                      id="dias-recomendados"
                      v-model="diasRecomendados"
                      readonly
                    />
                  </div>
                  <div>
                    <label for="dias-ordenados" class="form-label mt-5"
                      ><strong>Días ordenados</strong></label
                    >
                    <input
                      type="number"
                      class="form-control"
                      id="dias-ordenados"
                      v-model="diasOrdenados"
                    />
                  </div>
                </div>

                <!-- Análisis de la consulta -->
                <div class="col-md-6 mb-3">
                  <label for="analisis-consulta" class="form-label"
                    ><strong>Análisis de la consulta</strong></label
                  >
                  <textarea
                    class="form-control"
                    id="analisis-consulta"
                    rows="3"
                    v-model="analisisConsulta"
                    readonly
                  ></textarea>
                  <div class="mt-2">
                    <label for="fecha-finalizacion" class="form-label"
                      ><strong
                        >Fecha Finalización de incapacidad médica</strong
                      ></label
                    >
                    <input
                      type="date"
                      class="form-control"
                      id="fecha-finalizacion"
                      v-model="fechaFinalizacion"
                      readonly
                    />
                  </div>
                </div>
              </div>

              <hr />

              <div class="row mt-3">
                <!-- Observaciones de la incapacidad médica -->
                <div class="col-12 mb-3">
                  <label for="observaciones-incapacidad" class="form-label"
                    ><strong
                      >Observaciones de la incapacidad médica</strong
                    ></label
                  >
                  <textarea
                    class="form-control"
                    id="observaciones-incapacidad"
                    rows="3"
                    v-model="observacionesIncapacidad"
                  ></textarea>
                </div>
              </div>

              <!-- Botón para generar incapacidad médica -->
              <div class="mt-3">
                <button
                  type="button"
                  class="btn btn-custom btn-icon mb-2"
                  @click="generarIncapacidad"
                >
                  Generar
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
import { ref, computed, onMounted } from "vue";
import $ from "jquery";
import "datatables.net";
import "datatables.net-dt/css/dataTables.dataTables.css";
import { Modal } from "bootstrap";

export default {
  setup() {
    const motivoIncapacidad = ref("");
    const descripcionMotivo = ref("");
    const diagnosticoConsulta = ref("");
    const diasRecomendados = ref(0);
    const diasOrdenados = ref(0);
    const analisisConsulta = ref("");
    const fechaFinalizacion = ref("");
    const observacionesIncapacidad = ref("");
    const dataTable = ref(null);
    const modalBusquedaMotivo = ref(null);

    const fechaActual = new Date().toISOString().split("T")[0];

    const calcularFechaFinalizacion = computed(() => {
      if (diasOrdenados.value) {
        let fecha = new Date();
        fecha.setDate(fecha.getDate() + parseInt(diasOrdenados.value));
        return fecha.toISOString().split("T")[0];
      }
      return "";
    });

    const buscarMotivo = () => {
      modalBusquedaMotivo.value.show();
    };

    const seleccionarMotivo = (motivo) => {
      motivoIncapacidad.value = motivo.codigo;
      descripcionMotivo.value = motivo.descripcion;
      modalBusquedaMotivo.value.hide();
    };

    const generarIncapacidad = () => {
      if (!motivoIncapacidad.value || !diasOrdenados.value) {
        alert("Por favor, complete todos los campos obligatorios.");
        return;
      }

      const incapacidad = {
        motivoIncapacidad: motivoIncapacidad.value,
        descripcionMotivo: descripcionMotivo.value,
        diagnosticoConsulta: diagnosticoConsulta.value,
        diasRecomendados: diasRecomendados.value,
        diasOrdenados: diasOrdenados.value,
        analisisConsulta: analisisConsulta.value,
        fechaFinalizacion: calcularFechaFinalizacion.value,
        observacionesIncapacidad: observacionesIncapacidad.value,
        fechaGeneracion: fechaActual,
      };

      console.log("Incapacidad generada:", incapacidad);
      // Aquí puedes implementar la lógica para guardar la incapacidad en tu sistema
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

    onMounted(() => {
      modalBusquedaMotivo.value = new Modal(
        document.getElementById("modalBusquedaMotivo")
      );
      initDataTable();
    });

    return {
      motivoIncapacidad,
      descripcionMotivo,
      diagnosticoConsulta,
      diasRecomendados,
      diasOrdenados,
      analisisConsulta,
      fechaFinalizacion: calcularFechaFinalizacion,
      observacionesIncapacidad,
      dataTable,
      buscarMotivo,
      seleccionarMotivo,
      generarIncapacidad,
    };
  },
};
</script>
