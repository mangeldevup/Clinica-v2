<template>
  <!-- tab 2 -->
  <div
    class="tab-pane fade show"
    id="familiares"
    role="tabpanel"
    aria-labelledby="familiares-tab"
  >
    <div class="row mt-3">
      <div class="col-md-3">
        <!-- <button class="btn btn-custom btn-icon w-100" @click="adicionarNuevo">
          <i class="bi bi-plus-lg"></i> Adicionar nuevo
        </button> -->
        <div class="mt-3">
          <label for="cie10" class="form-label"
            >1. Seleccione antecente - CIE-10</label
          >
          <input
            type="text"
            class="form-control"
            id="cie10-2"
            v-model="cie10"
          />
          <button class="btn btn-custom btn-icon mt-2 w-100" @click="buscar">
            <i class="bi bi-search"></i> Buscar
          </button>
        </div>
        <div class="mt-3">
          <label for="fecha" class="form-label">2. Fecha de antecedente</label>
          <input
            type="date"
            class="form-control"
            id="fecha2"
            :value="fecha"
            @input="updateFecha"
          />
        </div>
        <div class="mt-3">
          <label for="familiar" class="form-label"
            >3. Familiar que lo presenta</label
          >
          <select class="form-select" id="familiar" v-model="familiar">
            <option value="" disabled selected>Seleccione un familiar</option>
            <option
              v-for="familiar in familiares"
              :key="familiar.id"
              :value="familiar.id"
            >
              {{ familiar.label }}
            </option>
          </select>
        </div>
        <button class="btn btn-custom btn-icon mt-2 w-100" @click="agregar">
          <i class="bi bi-floppy"></i> Agregar
        </button>
      </div>
      <div class="col-md-9">
        <h5 class="text-center mt-4">Registro de Antecedentes Familiares</h5>
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
</template>

<script>
import { familiares } from "../../../bd/bd.js";

import { ref, onMounted } from "vue";
import $ from "jquery";
import "datatables.net";
import "datatables.net-dt/css/dataTables.dataTables.css";

export default {
  name: "Tab2",
  props: {
    fecha: {
      type: String,
      required: true,
    },
  },
  setup() {
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
      familiares,
    };
  },
};
</script>
