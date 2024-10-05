<template>
  <div class="container">
    <form @submit.prevent="updateData">
      <div id="card-formulario" class="card mb-5">
        <div id="card-header-formulario" class="card-header py-3">
          <p class="text-primary m-0 fw-bold d-flex justify-content-between">
            <span class="titulo-formulario">
              <i class="bi bi-gender-male"></i> Antecedentes Andrológicos
            </span>
          </p>
        </div>
        <div class="card-body">
          <div class="antecedentes-andro">
            <!-- Sección de visualización de datos actuales -->
            <div class="current-data">
              <h3>Registro Actual</h3>
              <hr />
              <div class="data-grid">
                <div
                  v-for="(value, key) in currentData"
                  :key="key"
                  class="data-item"
                >
                  <span class="data-label">{{ labels[key] }}:</span>
                  <span class="data-value" :class="getValueClass(key, value)">{{
                    value
                  }}</span>
                </div>
              </div>
            </div>

            <!-- Formulario para actualizar datos -->
            <div class="update-form mt-4">
              <h3>Actualizar Datos</h3>
              <hr />
              <div class="form-grid">
                <div
                  v-for="(value, key) in formData"
                  :key="key"
                  class="form-group"
                >
                  <label :for="key">{{ labels[key] }}</label>
                  <input
                    v-if="!isSelect(key)"
                    :type="getInputType(key)"
                    :id="key"
                    v-model="formData[key]"
                    @blur="validateField(key)"
                  />
                  <select
                    v-else
                    :id="key"
                    v-model="formData[key]"
                    @blur="validateField(key)"
                  >
                    <option
                      v-for="option in selectOptions[key]"
                      :key="option.value"
                      :value="option.value"
                    >
                      {{ option.label }}
                    </option>
                  </select>
                  <small v-if="errors[key]" class="text-danger">{{
                    errors[key]
                  }}</small>
                </div>
              </div>
              <button
                type="submit"
                class="btn btn-custom btn-icon mt-4"
                :disabled="!isFormValid"
              >
                Actualizar datos
              </button>
            </div>

            <!-- Historial de cambios -->
            <div class="change-history mt-4">
              <h3>Historial de Cambios</h3>
              <hr />
              <ul v-if="changeHistory.length">
                <li v-for="(change, index) in changeHistory" :key="index">
                  {{ change.date }} - {{ labels[change.field] }}:
                  {{ change.oldValue }} → {{ change.newValue }}
                </li>
              </ul>
              <p v-else>No hay cambios registrados.</p>
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { ref, reactive, computed } from "vue";
import { antecedentesAndroData, labels, selectOptions } from "../../bd/bd.js";

export default {
  name: "AntecedentesAndro",
  setup() {
    const currentData = ref(antecedentesAndroData);
    const formData = reactive({ ...antecedentesAndroData });
    const errors = reactive({});
    const changeHistory = ref([]);

    const isFormValid = computed(() =>
      Object.values(errors).every((error) => !error)
    );

    const updateData = () => {
      if (isFormValid.value) {
        const changedFields = getChangedFields();
        if (Object.keys(changedFields).length > 0) {
          Object.keys(changedFields).forEach((key) => {
            changeHistory.value.unshift({
              date: new Date().toLocaleString(),
              field: key,
              oldValue: currentData.value[key],
              newValue: formData[key],
            });
            currentData.value[key] = formData[key];
          });

          Swal.fire("Éxito", "Datos actualizados correctamente", "success");
        } else {
          Swal.fire("Información", "No se detectaron cambios", "info");
        }
      } else {
        Swal.fire(
          "Error",
          "Por favor, corrija los errores antes de guardar",
          "error"
        );
      }
    };

    const validateField = (key) => {
      const value = formData[key];
      if (
        [
          "edadEspermaca",
          "edadInicioVidaSexual",
          "numeroParejasexuales",
        ].includes(key)
      ) {
        errors[key] = value < 0 ? "El valor no puede ser negativo" : "";
      } else {
        errors[key] = "";
      }
    };

    const getChangedFields = () => {
      return Object.keys(formData).reduce((acc, key) => {
        if (formData[key] !== currentData.value[key]) {
          acc[key] = formData[key];
        }
        return acc;
      }, {});
    };

    const getValueClass = (key, value) => {
      if (
        [
          "circuncision",
          "criptorquidea",
          "policionesNocturnas",
          "trastornosEreccion",
        ].includes(key)
      ) {
        return value === "Sí" ? "value-yes" : "value-no";
      }
      return "";
    };

    const isSelect = (key) =>
      [
        "circuncision",
        "criptorquidea",
        "policionesNocturnas",
        "trastornosEreccion",
        "orientacionSexual",
        "mProteccionSexual",
        "infTransmisionSexual",
      ].includes(key);

    const getInputType = (key) => {
      if (
        [
          "edadEspermaca",
          "edadInicioVidaSexual",
          "numeroParejasexuales",
        ].includes(key)
      )
        return "number";
      return "text";
    };

    return {
      currentData,
      formData,
      labels,
      selectOptions,
      errors,
      changeHistory,
      isFormValid,
      updateData,
      validateField,
      getValueClass,
      isSelect,
      getInputType,
    };
  },
};
</script>

<style scoped>
.antecedentes-go {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.current-data,
.update-form {
  background-color: #f8f9fa;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
}

.data-grid,
.form-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 15px;
}

.data-item,
.form-group {
  background-color: #ffffff;
  padding: 10px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.data-label,
label {
  font-weight: bold;
  display: block;
  margin-bottom: 5px;
}

input,
select {
  width: 100%;
  padding: 8px;
  border: 1px solid #ced4da;
  border-radius: 4px;
}

.btn-update {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.btn-update:hover {
  background-color: #0056b3;
}

.value-yes {
  color: green;
}

.value-no {
  color: red;
}

.alert {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 1000;
  padding: 15px;
  border-radius: 4px;
  transition: opacity 0.5s ease-in-out;
}

.change-history {
  max-height: 200px;
  overflow-y: auto;
}

.change-history ul {
  padding-left: 20px;
}

.change-history li {
  margin-bottom: 5px;
}
</style>
