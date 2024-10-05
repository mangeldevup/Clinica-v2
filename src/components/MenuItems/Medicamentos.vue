<template>
  <div class="container">
    <form>
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-capsule"></i> Medicamentos
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
              <div class="mt-3">
                <button
                  class="btn btn-custom btn-icon mb-2"
                  @click="abrirModalAgregarMedic"
                >
                  Agregar
                </button>
              </div>

              <h5 class="mt-4">Orden Medica</h5>
              <hr />

              <div class="table-responsive mt-3">
                <table class="table table-striped">
                  <thead class="bg-secondary text-white">
                    <tr>
                      <th>CUPS</th>
                      <th>Principio Activo</th>
                      <th>Nombre</th>
                      <th>Presentación</th>
                      <th>Posologia</th>
                      <th>Cantidad</th>
                      <th>Opc</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr
                      v-for="(medicamento, index) in medicamentos"
                      :key="index"
                    >
                      <td>{{ medicamento.cups }}</td>
                      <td>{{ medicamento.activo }}</td>
                      <td class="text-wrap">{{ medicamento.nombre }}</td>
                      <td class="text-wrap">{{ medicamento.presentacion }}</td>
                      <td class="text-wrap">{{ medicamento.posologia }}</td>
                      <td class="text-wrap">{{ medicamento.cantidad }}</td>
                      <td>
                        <button
                          class="custom-btn custom-delete-btn"
                          @click="eliminarMedicamento(index)"
                        >
                          <i class="fa-solid fa-trash-can"></i>
                        </button>
                      </td>
                    </tr>
                  </tbody>
                </table>
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
    <ModalAgregarMedic
      ref="modalAgregarMedic"
      @medic-agregado="onMedicamentoAgregado"
    />
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import $ from "jquery";
import "datatables.net";
import "datatables.net-dt/css/dataTables.dataTables.css";

import ModalAgregarMedic from "../ModalAgg/ModalAgregarMedic.vue";

export default {
  components: {
    ModalAgregarMedic,
  },
  setup() {
    const medicamentos = ref([]);
    const modalAgregarMedic = ref(null);

    const abrirModalAgregarMedic = () => {
      modalAgregarMedic.value.abrirModal();
    };

    const onMedicamentoAgregado = (nuevoMedicamento) => {
      medicamentos.value.push(nuevoMedicamento);
    };

    const eliminarMedicamento = (index) => {
      medicamentos.value.splice(index, 1);
    };

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
      medicamentos,
      abrirModalAgregarMedic,
      onMedicamentoAgregado,
      modalAgregarMedic,
      eliminarMedicamento,
      dataTable,
    };
  },
};
</script>
