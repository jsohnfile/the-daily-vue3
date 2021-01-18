<template>
    <div class="flex flex-wrap w-full">
        <div v-for="(color,index) in sliders" :key="color" class="absolute w-full" >
            <transition name="fade">
                <div 
                    v-if="currentSlide === index" 
                    class="w-full" 
                    :class="color" 
                    style="height:350px;"
                ></div>
            </transition> 
        </div>
        <div class="absolute w-full" style="height:340px;">
            <div class="absolute bottom-0 flex w-full justify-center">
                <div 
                    v-for="slider in sliders" 
                    :key="slider" 
                    class="w-4 h-4 rounded-full mx-2" 
                    :class="currentSlide == index ? 'bg-black-700':'bg-gray-300'"
                    @click="makeActive(index)"
                    ></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            currentSlide: 0,
            sliders:['bg-blue-600','bg-red-600','bg-green-600'],
            interval: "",
            isTitleShowing: true,
        }
    },
    methods:{
        makeActive(index){
            this.currentSlider = index;
        }
    },
    mounted(){
        this.interval = setInterval(() => {
            this.currentSlide = this.currentSlide === 2 ? 0: this.currentSlide + 1;
        }, 2000)
    },
    beforeUnmount(){
        clearInterval(this.interval)
    }
}
</script>

<style>
    .fade-enter-active,
    .fade-leave-active{
        transition: all 1s ease;
    }

    .fade-enter-from{
        opacity: 0;
        transform: translateX(-100%)
    }

    .fade-leave-to {
        opacity: 0;
        transform: translateX(100%);
    }
</style>