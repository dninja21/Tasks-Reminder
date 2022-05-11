<template>
 <div class="container">
 <Header title="Jobs Tracker"/>
 <AddTask @add-task="addTask"/> 
 <Tasks @toggle-reminder="toggleReminder"/>
 <Tasks @delete-task="deleteTask" :tasks="tasks"/>
 </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'



export default
{
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  
}, 

  data()
  {
    return {
        tasks:[],
    }
  },

  methods:{
    addTask(task)
    {
      this.tasks=[...this.tasks,task]

    },
    deleteTask(id) {
     
      this.tasks=this.tasks.filter((task)=>task.id!==id)
    },
    
    toggleReminder(id)
    {
      this.tasks=this.tasks.map((task)=>task.id ===id ?{... task, reminder:!task.reminder}:task)

    },

  },
  created() {
    this.tasks=[
      {
        id:1,
        text:'Doctors Appointment',
        day:'march',
        reminder:true,

      },
      {
        id:2,
        text:'Meeting at school',
        day:'march 3rd at 1.30',
        reminder:true,

      },
      {
        id:3,
        text:'applying for developer position',
        day:'April,2.30',
        reminder:true,

      },


    ]
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
