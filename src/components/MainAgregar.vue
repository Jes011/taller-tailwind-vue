<template>
  <div id="ventanaAgregar" v-bind:class="[establecido != 0 ? 'hidden' : '']">
    <form class="flex flex-col">
      <label>
        Código del proyecto
        <input
          v-model="codigo"
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            leading-tight
            focus:outline-none focus:shadow-outline
          "
          type="text"
        />
      </label>
      <label>
        Nombre
        <input
          v-model="nombre"
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            leading-tight
            focus:outline-none focus:shadow-outline
          "
          type="text"
        />
      </label>
      <label>
        Tipo de proyecto
        <select
          v-model="tipoProyecto"
          class="
            bg-white
            border border-gray-300
            text-gray-900 text-sm
            rounded-lg
            focus:ring-blue-500 focus:border-blue-500
            block
            w-full
            p-2.5
          "
        >
          <option disabled>Seleccione</option>
          <option>Investigación</option>
          <option>Extención</option>
        </select>
      </label>
      <label>
        Fecha inicio
        <input
          v-model="fechaInicio"
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            leading-tight
            focus:outline-none focus:shadow-outline
          "
          type="date"
        />
      </label>
      <label>
        Fecha finalización
        <input
          v-model="fechaFinalizacion"
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            leading-tight
            focus:outline-none focus:shadow-outline
          "
          type="date"
        />
      </label>
      <label>
        Dias de ejecución
        <input
          v-model="diasEjecucion"
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            leading-tight
            focus:outline-none focus:shadow-outline
          "
        />
      </label>
      <label>
        Responsable
        <input
          v-model="responsable"
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            leading-tight
            focus:outline-none focus:shadow-outline
          "
          type="text"
        />
      </label>
      <label>
        Presupuesto
        <input
          v-model="presupuesto"
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            leading-tight
            focus:outline-none focus:shadow-outline
          "
          type="text"
        />
      </label>
      <label>
        Tipo persona
        <div class="block">
          <input
            v-on:click="mostrarMenuPorTipo(1)"
            name="persona"
            type="radio"
          />Estudiante
          <input
            v-on:click="mostrarMenuPorTipo(0)"
            name="persona"
            type="radio"
          />Profesor
        </div>
      </label>
      <label v-bind:class="[menuPorTipo == 0 ? '' : 'hidden']">
        Tipo profesor
        <select
          v-model="tipoProfesor"
          class="
            bg-white
            border border-gray-300
            text-gray-900 text-sm
            rounded-lg
            focus:ring-blue-500 focus:border-blue-500
            block
            w-full
            p-2.5
          "
        >
          <option disabled>Seleccione</option>
          <option>Planta</option>
          <option>Transitorio</option>
        </select>
      </label>
      <label v-bind:class="[menuPorTipo == 1 ? '' : 'hidden']">
        Semestre estudiante
        <select
          v-model="semestreEstudiante"
          class="
            bg-white
            border border-gray-300
            text-gray-900 text-sm
            rounded-lg
            focus:ring-blue-500 focus:border-blue-500
            block
            w-full
            p-2.5
          "
        >
          <option disabled>Seleccione</option>
          <option>I</option>
          <option>II</option>
          <option>III</option>
          <option>IV</option>
          <option>V</option>
          <option>VI</option>
          <option>VII</option>
          <option>VIII</option>
          <option>IX</option>
          <option>X</option>
        </select>
      </label>
      <div
        v-on:click="agregar"
        class="
          w-full
          mt-4
          text-center
          bg-purple-600
          hover:bg-purple-700
          text-white
          font-bold
          py-2
          px-4
          rounded
        "
      >
        Registrar Proyecto
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "mainAgregar",
  data() {
    return {
      menuPorTipo: {
        type: Number,
        default: -1,
      },
      props:{
          dataAEditar:Object
      },
      codigo: "",
      nombre: "",
      tipoProyecto: "",
      fechaInicio: "",
      fechaFinalizacion: "",
      diasEjecucion: "",
      responsable: "",
      presupuesto: "",
      tipoPersona: "",
      tipoProfesor: "",
      semestreEstudiante: "",
    };
  },
  props: {
    establecido: {
      type: Number,
      default: -1,
    },
  },
  methods: {
    mostrarMenuPorTipo(menu) {
      this.menuPorTipo = menu;
      this.tipoPersona = menu == 0 ? "profesor" : menu == 1 ? "estudiante" : "";
    },
    agregar() {
      if (
        this.codigo &&
        this.nombre &&
        this.fechaInicio &&
        this.fechaFinalizacion &&
        this.diasEjecucion &&
        this.tipoProyecto &&
        this.responsable &&
        this.presupuesto &&
        this.tipoPersona &&
        (this.tipoProfesor || this.semestreEstudiante)
      ) {
        const fechaInicialVal = new Date("01-01-2022");
        const fechaFinalVal = new Date("12-30-2022");
        if (
          new Date(this.fechaInicio) < fechaInicialVal ||
          new Date(this.fechaFinalizacion) < fechaInicialVal ||
          fechaFinalVal < new Date(this.fechaFinalizacion)
        ) {
          alert(
            "La fecha de inicio y final debe ser mayor que 01-01-2022 y la fecha final debe ser menor que 31-12-2022"
          );
        } else {
          if (
            Number(this.presupuesto) < 10000000 ||
            Number(this.presupuesto) > 50000000
          ) {
            alert(
              "El presupuesto debe ser menor que de 50.000.000 y mayor que 10.000.000"
            );
          } else {
            this.$emit("addProyect", {
              codigo: this.codigo,
              nombre: this.nombre,
              tipoProyecto: this.tipoProyecto,
              fechaInicio: this.fechaInicio,
              fechaFinalizacion: this.fechaFinalizacion,
              diasEjecucion: this.diasEjecucion,
              responsable: this.responsable,
              presupuesto: this.presupuesto,
              tipoPersona: this.tipoPersona,
              tipoProfesor: this.tipoProfesor,
              semestreEstudiante: this.semestreEstudiante,
            });
          }
        }
      } else {
        alert("Debe llenar todos los campos");
      }
    },
  },
};
</script>

<style>
</style>