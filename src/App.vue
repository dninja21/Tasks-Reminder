<template>
 <div class="container">
 <Header @toggle-add-task="toggleAddTask" title="Jobs Tracker" :showAddTask="showAddTask"/>
 <div v-show="showAddTask">
    <AddTask @add-task="addTask"/> 
 </div> 
      
 
 
 <Tasks @toggle-reminder="toggleReminder"
  @delete-task="deleteTask" :tasks="tasks"/>
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
    AddTask,
  
}, 

  data()
  {
    return {
        tasks:[],
        showAddTask:false,
    }
  },

  methods:{
    async addTask(task)
    {
      const res=await fetch ('api/tasks', {
        method:'POST',
        headers:{
                  'Content-type':'application/json',        
               },
         body: JSON.stringify(task),
      })
      const data=await res.json()
      this.tasks=[...this.tasks,data]

    },
    toggleAddTask()
    {
      this.showAddTask=!this.showAddTask

    },
    
    async deleteTask(id) {
    

      if(confirm('Are you sure you want to delete')){
         
          const res= await fetch(`api/tasks/${id}`,{
          method:'DELETE',

       })
         res.status ===200 ? 
         (this.tasks=this.tasks.filter((task)=>task.id!==id)): 
         alert('Error Deleting Task');
     
      }
   
    },
    
    async toggleReminder(id)
    {
        const taskToToggle=await this.fetchTask(id)
        const updTask={... taskToToggle ,reminder:!taskToToggle.reminder}

        const res=await fetch(`api/tasks/${id}`,{
          method:'PUT',
          headers:{
                    'Content-type':'application/json',
          },
          body: JSON.stringify(updTask),
        })
       const data=await res.json()
       this.tasks=this.tasks.map((task)=>task.id ===id ?{... taskToToggle, reminder:data.reminder}
       :task
       )

    },

    async fetchTasks() {
      const res= await fetch('api/tasks')

      const data=await res.json()
      return data

    },
    async fetchTask(id) {
      const res= await fetch(`api/tasks/${id}`)

      const data=await res.json()
      return data

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
