<template>
    <header>
        <h1>{{title}}</h1>
        <Button v-show="homePage"
        @btn-click="$emit('toggle-add-task')"
        :text="showAddTask ?'close':'Add Task'"
        :color="showAddTask?'red':'green'" />

    </header>

</template>

<script>

import Button from "./Button"
 
    export default 
    {
    name: "Header",
    props: {
        title: String,
        showAddTask:Boolean,
    },
    components:{
        Button,
    },
    //for this add task button to be displayed if its on home page
    computed:{
        homePage()
        {
            if(this.$route.path === '/')
            {

                return true
            }
            else 
            {
                return false
            }

        }

    }

   
}


</script>


<style scoped>
    header {
            display:flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;

    }
</style>