<template>
  <div id="ventanaVer" v-bind:class="[establecido != 3 ? 'hidden' : '']">
    <form class="flex flex-col">
      <label>
        ID
        <input
          v-model="valorID"
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
      <div
        v-on:click="verProyect"
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
        Ver
      </div>
      <p class="text-center text-sm">
        Se abrira una ventana para mostrar los datos del proyecto
      </p>
    </form>
  </div>
</template>

<script>
export default {
  name: "mainVer",
  data() {
    return {
      valorID: "",
    };
  },
  props: {
    establecido: Number,
  },
  methods: {
    verProyect() {
      if (this.valorID) {
        this.$emit('verProyecto', this.valorID);
      }else{
          alert('Debe escribir algo en el campo');
      }
    },
  },
};
</script>

<style>
</style>