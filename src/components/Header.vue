<template>
    <header class="font-bold bg-slate-900 flex justify-between items-center flex-col lg:flex-row">
        <div class="flex items-center justify-between w-full lg:w-auto">
            <div class="flex items-center">
                <img class="w-16 lg:w-20" src="https://raw.githubusercontent.com/Jes011/Taller-tailwindcss_y_js/master/public/images/unicor.png">
                <span class=" ml-3">UNIVERSIDAD DE CORDOBA</span>
            </div>
            <img v-on:click="opMenu" class="lg:hidden cursor-pointer mr-2" src="https://raw.githubusercontent.com/Jes011/Taller-tailwindcss_y_js/master/public/images/menu.png">
        </div>
        <div v-bind:class="clase" class="bg-slate-900 lg:block w-full lg:w-1/3 ">
            <ul class=" flex justify-around flex-col lg:flex-row text-center w-full">
                <li>HOME</li>
                <li>ABOUT</li>
                <li>SERVICES</li>
                <li>PRICING</li>
            </ul>
        </div>
    </header>
</template>
<script>

export default{
    name:'Header',
    data(){
        return{
            clase:'hidden'
        }
    },
    methods:{
        opMenu(){
            (this.clase == 'hidden')?this.clase = '':this.clase = 'hidden';
        }
    }
}
</script>
