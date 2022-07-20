<template>
  <div id="ventanaEliminar" v-bind:class="getVisibilidad">
        <form class="flex flex-col">
            <label>
                ID
                <input v-model="valorEliminar"
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                     type="text">
            </label>
            <div v-on:click="eliminar"
                class="w-full mt-4 text-center bg-purple-600 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded">
                Eliminar</div>
        </form>
    </div>
</template>

<script>
export default {
    name:'mainEliminar',
    data(){
        return{
            valorEliminar:''
        }
    },
    props:{
        establecido:Number
    },
    methods:{
        eliminar(){
            if(this.valorEliminar){
                this.$emit('removeProyect',this.valorEliminar);
            }else{
                alert('Debe escribir el id');
            }
        }
    },
    computed:{
        getVisibilidad(){
            if(this.establecido==2){return''}else{return 'hidden'}
        }
    }
}
</script>

<style>

</style>