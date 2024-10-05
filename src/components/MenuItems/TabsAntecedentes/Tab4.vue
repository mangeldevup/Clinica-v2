<template>
  <!-- tab 4 -->
  <div
    class="tab-pane fade show"
    id="no-patologicos"
    role="tabpanel"
    aria-labelledby="no-patologicos-tab"
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
            id="cie10-4"
            v-model="cie10"
          />
          <button class="btn btn-custom btn-icon mt-2 w-100" @click="buscar">
            <i class="bi bi-search"></i> Buscar
          </button>
        </div>
        <!-- <div class="mt-3">
          <label for="fecha" class="form-label">2. Fecha de antecedente</label>
          <input type="date" class="form-control" id="fecha" v-model="fecha" />
        </div> -->
        <div class="mt-3">
          <label for="fecha" class="form-label">2. Fecha de antecedente</label>
          <input
            type="date"
            class="form-control"
            id="fecha4"
            :value="fecha"
            @input="updateFecha"
          />
        </div>
        <div class="mt-3">
          <label for="observaciones" class="form-label">3. Observaciones</label>
          <textarea
            class="form-control"
            id="observaciones4"
            rows="3"
            v-model="observaciones"
          ></textarea>
        </div>
        <button class="btn btn-custom btn-icon mt-2 w-100" @click="agregar">
          <i class="bi bi-floppy"></i> Agregar
        </button>
      </div>
      <div class="col-md-9">
        <h5 class="text-center mt-4">
          Registro de Antecedentes no Patológicos
        </h5>
        <!-- DataTable -->
        <div class="container">
          <div class="row">
            <div class="col-lg-12">
              <div class="table-responsive">
                <table
                  id="tab4"
                  class="table table-striped table-bordered"
                  style="width: 100%"
                >
                  <thead>
                    <tr>
                      <th>Name</th>
                      <th>Position</th>
                      <th>Office</th>
                      <th>Age</th>
                      <th>Start date</th>
                      <th>Salary</th>
                    </tr>
                  </thead>
                  <tbody></tbody>
                  <tfoot>
                    <tr>
                      <th>Name</th>
                      <th>Position</th>
                      <th>Office</th>
                      <th>Age</th>
                      <th>Start date</th>
                      <th>Salary</th>
                    </tr>
                  </tfoot>
                </table>
              </div>
            </div>
          </div>
        </div>
        <!-- Data Table -->
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted } from "vue";
import $ from "jquery";
import "datatables.net";
import "datatables.net-dt/css/dataTables.dataTables.css";

export default {
  setup() {
    onMounted(() => {
      $("#tab4").DataTable({
        paging: true, // Activar paginación
        searching: true, // Activar búsqueda
        ordering: true, // Activar ordenamiento por columnas
        pageLength: 10, // Número de filas por página
      });
    });
  },
  name: "Tab4",

  props: {
    fecha: {
      type: String,
      required: true,
    },
  },
};
</script>
