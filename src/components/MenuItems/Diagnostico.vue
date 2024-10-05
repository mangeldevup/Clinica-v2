<template>
  <div class="container">
    <form>
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-clipboard-check"></i> Diagnóstico
            </span>
            <span class="opciones-formulario"></span>
          </p>
        </div>

        <div class="card-body">
          <!-- Navegación con pestañas -->
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
            <!-- Tab de Actual -->
            <div
              class="tab-pane fade show active"
              id="home-tab-pane"
              role="tabpanel"
              aria-labelledby="home-tab"
              tabindex="0"
            >
              <div class="row mt-3">
                <div class="col-md-4 mb-3">
                  <label for="clasificacion-diagnostico" class="form-label"
                    >Clasificación diagnóstico</label
                  >
                  <select
                    class="form-select"
                    id="clasificacion-diagnostico"
                    v-model="diagnostico.clasificacion"
                  >
                    <option disabled value="">Seleccione</option>
                    <option
                      v-for="clasificacion in Diagnostico.clasificacionesDiagnostico"
                      :key="clasificacion.id"
                      :value="clasificacion.id"
                    >
                      {{ clasificacion.label }}
                    </option>
                  </select>
                </div>
                <div class="col-md-4 mb-3">
                  <label for="finalidad-consulta" class="form-label"
                    >Finalidad de la consulta</label
                  >
                  <select
                    class="form-select"
                    id="finalidad-consulta"
                    v-model="diagnostico.finalidad"
                  >
                    <option disabled value="">Seleccione</option>
                    <option
                      v-for="finalidad in Diagnostico.finalidadesConsulta"
                      :key="finalidad.id"
                      :value="finalidad.id"
                    >
                      {{ finalidad.label }}
                    </option>
                  </select>
                </div>
                <div class="col-md-4 mb-3">
                  <label for="causa-externa" class="form-label"
                    >Causa Externa</label
                  >
                  <select
                    class="form-select"
                    id="causa-externa"
                    v-model="diagnostico.causaExterna"
                  >
                    <option disabled value="">Seleccione</option>
                    <option
                      v-for="causa in Diagnostico.causasExternas"
                      :key="causa.id"
                      :value="causa.id"
                    >
                      {{ causa.label }}
                    </option>
                  </select>
                </div>
              </div>
              <div class="row mt-3">
                <div class="col-md-3">
                  <h6>Diagnóstico Principal</h6>
                  <button
                    class="btn btn-custom btn-icon mb-2"
                    @click="buscarCIE10('principal')"
                  >
                    BUSCAR CIE-10
                  </button>
                </div>
                <div class="col-md-9">
                  <label for="descripcion-principal" class="form-label"
                    >Descripción</label
                  >
                  <textarea
                    class="form-control"
                    id="descripcion-principal"
                    rows="3"
                    disabled
                    v-model="diagnostico.principal.descripcion"
                  ></textarea>
                </div>
              </div>

              <div class="row mt-3">
                <div class="col-md-3">
                  <h6>Relacionado Primario</h6>
                  <button
                    class="btn btn-custom btn-icon mb-2"
                    @click="buscarCIE10('primario')"
                  >
                    BUSCAR CIE-10
                  </button>
                </div>
                <div class="col-md-9">
                  <label for="descripcion-primario" class="form-label"
                    >Descripción</label
                  >
                  <textarea
                    class="form-control"
                    id="descripcion-primario"
                    rows="3"
                    disabled
                    v-model="diagnostico.primario.descripcion"
                  ></textarea>
                </div>
              </div>

              <div class="row mt-3">
                <div class="col-md-3">
                  <h6>Relacionado Secundario</h6>
                  <button
                    class="btn btn-custom btn-icon mb-2"
                    @click="buscarCIE10('secundario')"
                  >
                    BUSCAR CIE-10
                  </button>
                </div>
                <div class="col-md-9">
                  <label for="descripcion-secundario" class="form-label"
                    >Descripción</label
                  >
                  <textarea
                    class="form-control"
                    id="descripcion-secundario"
                    rows="3"
                    disabled
                    v-model="diagnostico.secundario.descripcion"
                  ></textarea>
                </div>
              </div>

              <div class="row mt-3">
                <div class="col-md-3">
                  <h6>Relacionado Terciario</h6>
                  <button
                    class="btn btn-custom btn-icon mb-2"
                    @click="buscarCIE10('terciario')"
                  >
                    BUSCAR CIE-10
                  </button>
                </div>
                <div class="col-md-9">
                  <label for="descripcion-terciario" class="form-label"
                    >Descripción</label
                  >
                  <textarea
                    class="form-control"
                    id="descripcion-terciario"
                    rows="3"
                    disabled
                    v-model="diagnostico.terciario.descripcion"
                  ></textarea>
                </div>
              </div>

              <div class="row mt-3">
                <div class="col-md-3">
                  <h6>Relacionado Cuartenario</h6>
                  <button
                    class="btn btn-custom btn-icon mb-2"
                    @click="buscarCIE10('cuartenario')"
                  >
                    BUSCAR CIE-10
                  </button>
                </div>
                <div class="col-md-9">
                  <label for="descripcion-cuartenario" class="form-label"
                    >Descripción</label
                  >
                  <textarea
                    class="form-control"
                    id="descripcion-cuartenario"
                    rows="3"
                    disabled
                    v-model="diagnostico.cuartenario.descripcion"
                  ></textarea>
                </div>
              </div>
            </div>

            <!-- Tab de Historial -->
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
import { Diagnostico } from "../../bd/bd.js";
import { ref, onMounted } from "vue";
import $ from "jquery";
import "datatables.net";
import "datatables.net-dt/css/dataTables.dataTables.css";

export default {
  data() {
    return {
      Diagnostico,
      diagnostico: {
        clasificacion: "",
        finalidad: "",
        causaExterna: "",
        principal: { codigo: "", descripcion: "" },
        primario: { codigo: "", descripcion: "" },
        secundario: { codigo: "", descripcion: "" },
        terciario: { codigo: "", descripcion: "" },
        cuartenario: { codigo: "", descripcion: "" },
      },
    };
  },
  methods: {
    buscarCIE10(tipo) {
      console.log(`Buscando CIE-10 para diagnóstico ${tipo}`);
    },
  },
  setup() {
    // Data Table
    const dataTable = ref(null);

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
      dataTable,
    };
  },
};
</script>
