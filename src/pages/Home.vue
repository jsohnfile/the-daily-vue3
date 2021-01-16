<template>
    <div class="m-auto flex flex-col items-center justify-center h-screen">
        <h1 class=" text-4xl text-center">The Daily Vue</h1>
        <h1 class=" text-4xl text-center my-4">{{ today() }}</h1>
        <h1 class=" text-4xl text-center my-4">{{ hour }} : {{ minute }} : {{ second }}  {{ periodSymbol }}</h1>
    </div>
</template>

<script>
import today from "../utilities/mixins/today";
export default {
    data() {
        return{
            hour:'--',
            minute:'--',
            second:'--',
            periodSymbol: '--',
        }
    },

    mixins:[today],
    
    mounted(){
        setInterval(() => {
            const todayTime = new Date();
            if (todayTime.getHours() > 12 && todayTime.getHours() < 25){
                this.periodSymbol = 'PM';
            }else {
                this.periodSymbol = 'AM';
            }
            this.hour = zeroPadding(period(todayTime.getHours()), 2);
            this.minute = zeroPadding(todayTime.getMinutes(), 2);
            this.second = zeroPadding(todayTime.getSeconds(), 2);
        }, 1000);
        function zeroPadding(num, digit) {
            let zero = '';
            for(let i = 0; i < digit; i++) {
                zero += '0';
            }
            return (zero + num).slice(-digit);
        }
        function period(ampm){
            if (ampm > 12 && ampm < 25){
                return ampm - 12;
            }
        }
    }

}
</script>
<style>

</style>