<template>
    <div
        class=" 
          fixed
          w-full
          h-full
          top-0
          transparente
          flex
          justify-center
          items-center
        "
    >
        <div class="bg-slate-900 p-5 min-w-max">
          <div>
            <h3 class="text-5xl font-bold">
              {{data.nombre}}
            </h3>
          </div>
          <div class="flex flex-col">
            <div>Codigo: <span>{{data.codigo}}</span></div>
            <div>
              Tipo proyecto: <span>{{data.tipoProyecto}}</span>
            </div>
            <div>
              Responsable: <span>{{data.responsable}}</span>
            </div>
            <div>
              Presupuesto: <span>{{data.presupuesto}}</span>
            </div>
            <div>Fecha inicion: <span>{{data.fechaInicio}}</span></div>
            <div>Fecha fin: <span>{{data.fechaFinalizacion}}</span></div>
            <div>
              Dias de ejecucion: <span>{{data.diasEjecucion}}</span>
            </div>
            <div>
              Tipo de persona: <span class="ml-5">{{data.tipoPersona}}</span>
            </div>
            <div v-show="data.tipoProfesor" id="contenedorTipoProfesorVentanaEmergente">
              Tipo de profesor: <span>{{data.tipoProfesor}}</span>
            </div>
            <div v-show="data.semestreEstudiante" id="contenedorSemestreEstudianteVentanaEmergente">
              Semestre estudiante: <span>{{data.semestreEstudiante}}</span>
            </div>
          </div>
          <div
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
            v-on:click="cerrarVentana"
          >
            OK
          </div>
        </div>
    </div>
</template>
<script>

export default{
    props:{
        data:Object
    },
    methods:{
        cerrarVentana(){
            this.$emit('ventanaDialogo',false);
        }
    }
}
</script>