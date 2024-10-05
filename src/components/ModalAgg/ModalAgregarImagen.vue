<template>
  <div
    class="modal fade"
    id="modalAgregarImagen"
    tabindex="-1"
    aria-labelledby="modalAgregarImagenLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content">
        <div id="headerm-general" class="modal-header">
          <h5 class="modal-title" id="modalAgregarImagenLabel">
            Agregar Nueva Imagen
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
          <form @submit.prevent="agregarImagen">
            <div class="mb-3">
              <label for="cups" class="form-label">CUPS</label>
              <input
                type="number"
                class="form-control"
                id="cups"
                v-model="nuevaImagen.cups"
                required
              />
            </div>
            <div class="mb-3">
              <label for="nombre" class="form-label">Nombre</label>
              <input
                type="text"
                class="form-control"
                id="nombre"
                v-model="nuevaImagen.nombre"
                required
              />
            </div>
            <div class="mb-3">
              <label for="descripcion" class="form-label">Descripción</label>
              <textarea
                class="form-control"
                id="descripcion"
                v-model="nuevaImagen.descripcion"
                rows="3"
              ></textarea>
            </div>
            <div class="mb-3">
              <label for="cantidad" class="form-label">Cantidad</label>
              <input
                type="number"
                class="form-control"
                id="cantidad"
                v-model="nuevaImagen.cantidad"
                required
              />
            </div>
            <div class="mb-3">
              <label for="imagen" class="form-label">Imagen</label>
              <input
                type="file"
                class="form-control"
                id="imagen"
                @change="onFileChange"
                accept="image/*"
                required
              />
            </div>
            <div class="modal-footer d-flex justify-content-between">
              <button type="submit" class="btn btn-custom btn-icon mb-2">
                Agregar
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import { Modal } from "bootstrap";

export default {
  name: "ModalAgregarImagen",
  emits: ["imagen-agregada"],
  setup(props, { emit }) {
    const nuevaImagen = ref({
      cups: "",
      nombre: "",
      descripcion: "",
      cantidad: "",
      imagen: null,
      fecha: new Date().toISOString().split("T")[0], // Fecha actual
    });

    const modalInstance = ref(null);

    onMounted(() => {
      modalInstance.value = new Modal(
        document.getElementById("modalAgregarImagen")
      );
    });

    const abrirModal = () => {
      modalInstance.value.show();
    };

    const onFileChange = (e) => {
      const file = e.target.files[0];
      nuevaImagen.value.imagen = file;
    };

    const agregarImagen = () => {
      emit("imagen-agregada", { ...nuevaImagen.value });
      nuevaImagen.value = {
        cups: "",
        nombre: "",
        descripcion: "",
        cantidad: "",
        imagen: null,
        fecha: new Date().toISOString().split("T")[0],
      };
      modalInstance.value.hide();
    };

    return {
      nuevaImagen,
      abrirModal,
      agregarImagen,
      onFileChange,
    };
  },
};
</script>
