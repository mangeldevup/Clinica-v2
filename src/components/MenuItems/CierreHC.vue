<template>
  <div class="cierre-hc-container">
    <div class="alerta-wrapper">
      <div class="icono-atencion">
        <i class="fa-solid fa-triangle-exclamation"></i>
      </div>
      <div class="contenido-mensaje">
        <h3>¡Atención!</h3>
        <hr />
        <p>
          Está a punto de cerrar la historia clínica de la consulta realizada
          previamente. Este proceso almacenará la información tal como se
          encuentra actualmente y no podrá editarse nuevamente. Si está seguro
          de cerrar el documento, continúe. De lo contrario, verifique la
          información consignada.
        </p>
        <p>
          Se solicitará el ping para verificar su identidad y firmar el
          documento.
        </p>
      </div>
      <div class="boton-wrapper">
        <button @click="confirmarCierre" class="btn-firmar">
          <i class="fa-solid fa-check"></i> Firmar HC y Guardar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CierreHC",
  methods: {
    confirmarCierre() {
      if (
        confirm(
          "¿Está seguro que desea firmar y cerrar la historia clínica? Esta acción no se puede deshacer."
        )
      ) {
        localStorage.removeItem("selectedMenuItems");
        alert("La historia clínica ha sido cerrada exitosamente.");
        window.location.reload();
      }
    },
  },
};
</script>

<style scoped>
.cierre-hc-container {
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.alerta-wrapper {
  display: flex;
  align-items: flex-start;
  padding: 20px;
  border: 1px solid #ddd;
  background-color: #fff;
  border-radius: 8px;
  width: 100%;
  max-width: 1200px;
  flex-wrap: wrap;
}

.icono-atencion {
  flex: 0 0 auto;
  margin-right: 20px;
  color: #d9534f;
  font-size: 98px;
  margin-top: -20px;
}

.contenido-mensaje {
  flex: 1 1 auto;
  margin-right: 20px;
  margin-top: -25px;
}

.contenido-mensaje h3 {
  font-size: 20px;
  font-weight: bold;
  color: #d9534f;
  margin-bottom: 10px;
}

.contenido-mensaje p {
  margin: 0;
  font-size: 16px;
  line-height: 1.5;
  color: #333;
}

.boton-wrapper {
  flex: 0 0 auto;
  display: flex;
  align-items: center;
}

.btn-firmar {
  background-color: #f8d7da;
  color: #d9534f;
  border: 1px solid #d9534f;
  padding: 10px 20px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 20px;
  margin-bottom: 20px;
}

.btn-firmar i {
  margin-right: 8px;
}

.btn-firmar:hover {
  background-color: #d9534f;
  color: #fff;
}

@media (max-width: 768px) {
  .alerta-wrapper {
    flex-direction: column;
    align-items: center;
  }

  .icono-atencion {
    margin-bottom: 15px;
    font-size: 40px;
  }

  .contenido-mensaje h3 {
    text-align: center;
  }

  .contenido-mensaje p {
    text-align: justify;
  }

  .boton-wrapper {
    margin-top: 15px;
  }
}
</style>
