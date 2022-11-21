<template>
<Popup v-show="isAddModalVisible" @close="closeAddModal" 
:existing_description = description
:existing_deadline = deadline
:existing_priority = priority
:tasks = "tasks"
@submitTask = "submitTask"
@close = "closeAddModal"/>

<editpopup v-show="isEditModalVisible" @close="closeEditModal"/>


  <div class = "container-fluid">
  <div class="card">
            <div class = "panel panel-primary">

  <div class = "d-flex justify-content-between align-items-center"> 
   <div class = "col-sm-11">
    <h5 class = "text-center"> FRAMEWORKS </h5>
    </div>
    <div class = "col-md-1"> 
    <button type = "button" @click = "showAddModal" class = "btn btn-primary btn-sm"> <span class = "fa-solid fa-circle-plus"> </span> Add</button> 
    </div>
    </div>
    </div>
    </div>

    <!-- Input -->
    <div class = "d-flex"> 
    <input v-model = "task" type = "text" placeholder = "Enter Task" class = "form-control">
    <button @click = "submitTask" class = "btn btn-warning rounded-0"> SUBMIT </button>
    </div>

    <!-- Task table -->
    <table class="table table-bordered">
  <thead>
    <tr>
      <th scope="col" class = "text-center">Title</th>
      <th scope="col" class = "text-center">Description</th>
      <th scope="col" class = "text-center">Deadline</th>
      <th scope="col" class = "text-center">Priority</th>
      <th scope="col" class = "text-center">Is Complete</th>
      <th scope="col" class = "text-center">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for = "(task, index) in tasks" :key ="index">
    <td> {{task.title}} </td>
    <td> {{task.description}} </td>
    <td> {{task.deadline}} </td>
    <td><span> {{task.priority}} </span> </td>
    <td align = "center"> 
      <label class="container">
      <input type="checkbox" checked="checked">
      <span class="checkmark"></span>
    </label>
</td>
    <td>
    <div class = "text-center">
    <button class = "btn btn-primary btn-sm w-75" @click = "showEditModal" > 
    <span class = "fa fa-pen"></span> Update </button>
    </div>
    <div class = "text-center" @click = "deleteTask(index)">
    <button class = "btn btn-danger btn-sm w-75"> 
    <span class = "fa fa-circle-xmark"></span> Delete </button>
    </div>
    </div>
     </td>

    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
import Popup from './popup';
import editpopup from './editpopup'; 
export default {
  name: 'Todo',
  props: {
    msg: String,
  },

  components: {
    Popup,
    editpopup
  },

  data(){
    return{
      isAddModalVisible: false, 
      isEditModalVisible: false,
      task: '', 
      editedTask: null, 
      availablePriorities: ['low', 'med', 'high'], 
      tasks: [
      {
        taskIndex: null, 
        title: '' , 
        description: '',
        deadline: '',
        priority: "low",
      }
      ]
    }
    },

    methods: {
      submitTask(){
        if(this.task.length === 0) return;
        
        if(this.editedTask === null){
        this.tasks.push({
          title: title,
          description: description, 
          deadline: deadline,
          priority: priority,
          isComplete: false,
        });
        }
        else{
          this.tasks[this.editedTask].title = this.task;
          this.editedTask = null; 
        }
        this.task = ''; 

      },

      deleteTask(index){
        this.tasks.splice(index, 1); 
      },

      editTask(index){
        this.task = this.tasks[index].title; 
        this.editedTask = index; 
      },
      showAddModal() {
        this.isAddModalVisible = true;
    },
       closeAddModal() {
        this.isAddModalVisible = false;
      },

       showEditModal() {
        this.isEditModalVisible = true;
    },
       closeEditModal() {
        this.isEditModalVisible = false;
      },
    }
};
</script>

<style>
.todo-header{
  position: relative;
  border-bottom: 1px solid #eeeeee;
  background: blue;
  color: white;
  justify-content: center;
}
</style> 

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
