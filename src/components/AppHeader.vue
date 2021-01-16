<template>
    <nav class="w-full bg-gradient-to-r from-blue-800 to-blue-400 text-white px-4 py-2">
        <router-link 
            class="mx-4" 
            v-for="item in list" :key="item.to" 
            :to="item.to">{{ item.title }}</router-link>

    </nav>
</template>

<script>
export default {
    data() {
        return{
            list: [
                {title:"The Daily",to:"/"},
                {title:"Todos",to:"/todos"},
                {title:"Calendar",to:"/calendar"},
                {title:"Markdown",to:"/markdown"},
                {title:"Slider",to:"/slider"},
            ]
        }
    }
}
</script>