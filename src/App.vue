<template>
  <div id="app" class="container text-center py-3">
    <main>
      <h1>Citas médicas</h1>
      <form class="border rounded my-3 p-4" @submit.prevent="agregarCita">
        <div class="d-flex justify-content-around">
          <!--PACIENTES-->
          <div>
            <label
              for=""
              class="form-label"
              :class="!cita.paciente ? 'text-danger' : ''"
              >Paciente:
            </label>
            <input type="text" class="form-control" v-model="cita.paciente" />
          </div>
          <!--FECHA-->
          <div>
            <label
              for=""
              class="form-label"
              :class="!cita.fecha ? 'text-danger' : ''"
              >Fecha:
            </label>
            <input type="date" class="form-control" v-model="cita.fecha" />
          </div>
          <!--HORA-->
          <div>
            <label
              for=""
              class="form-label"
              :class="!cita.hora ? 'text-danger' : ''"
              >Hora:
            </label>
            <input type="time" class="form-control" v-model="cita.hora" />
          </div>
          <!--GRAVEDAD-->
          <div>
            <label
              for=""
              class="form-label"
              :class="!cita.gravedad ? 'text-danger' : ''"
              >Gravedad:
            </label>
            <select name="" id="" class="form-select" v-model="cita.gravedad">
              <option
                :value="gravedad"
                v-for="(gravedad, index) in gravedades"
                :key="index"
              >
                {{ gravedad }}
              </option>
            </select>
          </div>
          <!--MOTIVO-->
          <div>
            <label
              for=""
              class="form-label"
              :class="!cita.motivo ? 'text-danger' : ''"
              >Motivo:
            </label>
            <input type="text" class="form-control" v-model="cita.motivo" />
          </div>
        </div>
        <div class="py-4">
          <button
            type="submit"
            class="btn btn-light"
            :disabled="
              !cita.paciente ||
              !cita.fecha ||
              !cita.hora ||
              !cita.gravedad ||
              !cita.motivo
            "
          >
            Agregar
          </button>
        </div>
      </form>
      <div>
        <p class="text-danger" v-if="citas.length < 1">
          Aún no hay consultas registradas
        </p>
        <div v-else class="row g-2">
          <div class="col-3" v-for="(cita, index) in citas" :key="index">
            <CardComp :cita="cita" @EliminarCita="eliminarCitaHandler(index)" />
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import CardComp from "./components/CardComp.vue";

export default {
  name: "App",
  // COMPONENTS
  components: {
    CardComp,
  },
  // DATA
  data() {
    return {
      citas: [],
      cita: {
        paciente: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      },
      gravedades: ["Baja", "Media", "Alta"],
    };
  },
  // METHODS
  methods: {
    agregarCita() {
      this.citas.push(this.cita);
      this.cita = {};
    },
    eliminarCitaHandler(index) {
      if (confirm("Estas seguro que deseas eliminar esta cita?")) {
        this.citas.splice(index, 1);
      }
    },
  },
};
</script>

<style>
</style>
