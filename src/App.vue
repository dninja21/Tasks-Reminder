<template>
 <div class="container">
 <Header @toggle-add-task="toggleAddTask" title="Jobs Tracker" :showAddTask="showAddTask"/>
 
  <router-view :showAddTask="showAddTask"></router-view>
 <Footer/>
 </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'



export default
{
  name: 'App',
  components: {
    Header,
    Footer
  
}, 

  data()
  {
    return {
        showAddTask:false,
    }
  },

  methods:{

     toggleAddTask()
    {
      this.showAddTask=!this.showAddTask

    }

    },
  
  
  async created() 
  {
    this.tasks=await this.fetchTasks()
  }



}
</script>

<style>

.container {

 max-width:"500px";
 margin:30px auto;
 overflow:auto;
 min-height:300px;
 border:1px solid steelblue;
 padding:30px;
 border-radius:30px

}

.btn{
    width: 140px;
    height: 80px;
    border: none;
    outline: none;
    background: #2f2f2f;
    color: #fff;
    font-size: 15px;
    border-radius: 40px;
    text-align: center;
    box-shadow: 0 6px 20px -5px rgba(0,0,0,0.4);
    position: relative;
    overflow: hidden;
    cursor: pointer;
}



</style>
