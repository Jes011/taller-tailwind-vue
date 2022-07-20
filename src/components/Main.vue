<template>
  <main class="bg-gray-800">
    <div class="text-center">
      <h2 class="text-3xl lg:text-5xl text-center font-bold text-white">
        Mis proyectos
      </h2>
      <span>Administracion general de mis poroyectos</span>
    </div>
    <div class="flex flex-col justify-around gap-2 lg:flex-row w-full mt-5">
      <div class="w-full lg:w-4/12">
        <div class="bg-purple-800 flex justify-around">
          <h3
            v-on:click="cambiarVentana(0)"
            class="
              text-lg
              lg:text-xl
              text-center
              font-bold
              text-purple-300
              hover:text-purple-50
              cursor-pointer
            "
          >
            Agregar
          </h3>
          <h3
            v-on:click="cambiarVentana(2)"
            class="
              text-lg
              lg:text-xl
              text-center
              font-bold
              text-purple-300
              hover:text-purple-50
              cursor-pointer
            "
          >
            Eliminar
          </h3>
          <h3
            v-on:click="cambiarVentana(1)"
            class="
              text-lg
              lg:text-xl
              text-center
              font-bold
              text-purple-300
              hover:text-purple-50
              cursor-pointer
            "
          >
            Editar
          </h3>
          <h3
            v-on:click="cambiarVentana(3)"
            class="
              text-lg
              lg:text-xl
              text-center
              font-bold
              text-purple-300
              hover:text-purple-50
              cursor-pointer
            "
          >
            Ver
          </h3>
        </div>
        <div class="bg-slate-900 p-5">
          <mainAgregar :establecido="establecido" @addProyect="addProyect" />
          <mainEditar :establecido="establecido" :data="dataAEditar" @preEditar="preEditarProyecto" @editarProyecto="editarProyecto" />
          <mainEliminar
            :establecido="establecido"
            @removeProyect="removeProyect"
          />
          <mainVer :establecido="establecido" @verProyecto="verProyecto"/>
        </div>
      </div>
      <div class="flex flex-row justify-center w-12/12">
        <div class="w-full">
          <div class="shadow-md h-screen overflow-y-scroll">
            <table id="table" class="w-full text-sm text-left text-purple-300">
              <thead class="text-xs text-purple-300 uppercase bg-purple-800">
                <tr>
                  <th scope="col" class="px-6 py-3">id</th>
                  <th scope="col" class="px-6 py-3">Nombre</th>
                  <th scope="col" class="px-6 py-3">Responsable</th>
                  <th scope="col" class="px-6 py-3">Fecha inicio</th>
                  <th scope="col" class="px-6 py-3">Fecha fin</th>
                  <th scope="col" class="px-6 py-3">Dias de ejecución</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  class="bg-slate-900 border-b"
                  v-for="(proyecto1, index) in proyectos"
                  :key="index"
                >
                  <th
                    scope="row"
                    class="
                      px-6
                      py-4
                      font-medium
                      text-gray-100
                      whitespace-nowrap
                    "
                  >
                    {{ proyecto1.codigo }}
                  </th>
                  <td class="px-6 py-4">
                    {{ proyecto1.nombre }}
                  </td>
                  <td class="px-6 py-4">
                    {{ proyecto1.responsable }}
                  </td>
                  <td class="px-6 py-4">
                    {{ proyecto1.fechaInicio }}
                  </td>
                  <td class="px-6 py-4">
                    {{ proyecto1.fechaFinalizacion }}
                  </td>
                  <td class="px-6 py-4">
                    {{ proyecto1.diasEjecucion }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
    <!-- VENTANA DE DIALOGO QUE OPACA EL FONDO-->
    <MainVentanaDialog v-if="ventanaDialogo" v-bind:data="dataVentanaDialog" @ventanaDialogo="opVentanaDialogo" />
  </main>
</template>

<script>
import mainAgregar from "./MainAgregar.vue";
import mainEditar from "./MainEditar.vue";
import mainEliminar from "./MainEliminar.vue";
import mainVer from "./MainVer.vue";
import MainVentanaDialog from "./MainVentanaDialog.vue";

export default {
  components: {
    mainAgregar,
    mainEditar,
    mainEliminar,
    mainVer,
    MainVentanaDialog,
  },
  data() {
    return {
      establecido: 0,
      ventanaDialogo: false,
      proyectos: [],
      dataVentanaDialog: null,
      dataAEditar:null
    };
  },
  methods: {
    cambiarVentana(ventana) {
      this.dataAEditar = null;
      this.establecido = ventana;
    },
    addProyect(proyect) {
      if (
        this.proyectos.find((proyecto) => proyecto.codigo == proyect.codigo)
      ) {
        alert("Este codigo ya esta registrado");
      } else {
        this.proyectos.push(proyect);
        alert("Proyecto agregado");
      }
    },
    removeProyect(codigo) {
      const elemento = this.proyectos.find(
        (proyecto) => proyecto.codigo == codigo
      );
      if (elemento) {
        this.proyectos.splice(
          this.proyectos.indexOf(elemento),
          this.proyectos.indexOf(elemento) + 1
        );
        alert("Proyecto eliminado");
      } else {
        alert("Codigo no encontrado");
      }
    },
    opVentanaDialogo(valor) {
      this.ventanaDialogo = valor;
    },
    verProyecto(codigo) {
      const proyecto = this.proyectos.find(
        (proyect) => proyect.codigo == codigo
      );
      if (proyecto) {
        this.ventanaDialogo = true;
        this.dataVentanaDialog = proyecto;
      }else{
          alert('proyecto no encontrado');
      }
    },
    preEditarProyecto(codigo){
        const temporal = this.proyectos.find(proyect=>proyect.codigo==codigo);
        if(temporal){
            this.dataAEditar = temporal;
        }else{
            alert('Proyecto no encontrado');
        }
    },
    editarProyecto(afData){
        this.proyectos.splice(this.proyectos.indexOf(this.dataAEditar),1,afData);
        console.log(this.proyectos);
        alert('Editado correctamente');
    }
    
  },
};
</script>

<style>
</style>