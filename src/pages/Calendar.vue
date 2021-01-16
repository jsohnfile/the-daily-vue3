<template>
    <div class="m-auto flex flex-col items-center">
        <div class="calendar-subcontainer">
            <h1 class="text-4xl my-10 text-center">Calendar</h1>
            <section class="mx-2 flex justify-between">
                <h2 class="font-bold">{{ currentMonthName }} </h2>
                <h2 class="font-bold">{{ currentYear }} </h2>
            </section>
            <section class="flex">
                <div class="text-center my-2" style="width: 64px" v-for="day in days" :key="day">{{day}}</div>
            </section>
            <section class="flex flex-wrap" style="width: 460px; height:144px">
                <div class="text-center" style="width: 64px"  v-for="num in startDay()" :key="num"></div>
                <div class="text-center" style="width: 64px"  v-for="num in daysInMonth()" :key="num" :class="currentDateClass(num)">{{ num }}</div>
            </section>
            <section class="flex justify-between my-4">
                <button class="px-2 border rounded bg-gray-100" @click="prev">Prev</button>
                <button class="px-2 border rounded bg-gray-100" @click="next">Next</button>
            </section>
            <h1 class="text-blue-500 font-bold text-center my-4">Today is <span class="italic">{{ today() }}</span></h1>
        </div> 
    </div>
</template>

<script>
import today from "../utilities/mixins/today"
export default {
    mixins: [today],
    data() {
        return {
            currentDate: new Date().getDate(),
            currentMonth: new Date().getMonth(),
            currentYear: new Date().getFullYear(),
            days: ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'],
        }
    },
    methods:{
        daysInMonth(){
            return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();  
        },
        startDay() {
            return new Date(this.currentYear, this.currentMonth, 1).getDay();
        },
        next() {
            if(this.currentMonth === 11){
                this.currentMonth = 0;
                this.currentYear++;
            }else{
                this.currentMonth++;
            }

        },
        prev() {
            if(this.currentMonth=== 0){
                this.currentMonth = 11;
                this.currentYear--;
            }else{
                this.currentMonth--;
            }
        },
        currentDateClass(num) {
            const calendarFullDate = new Date(this.currentYear, this.currentMonth, num).toDateString();
            const currentFullDate = new Date().toDateString();
            return calendarFullDate === currentFullDate ? 'text-red-500 font-bold' : '';
        }
    },
    computed: {
        currentMonthName() {
            return new Date(this.currentYear, this.currentMonth).toLocaleString("default", {
                month: "long"});
        }
    }
} 
</script>

<style>

</style>