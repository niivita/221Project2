
<template>
  <div class="modal-backdrop">
    <div class="modal" id="addModal" role="dialog">
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">
              <span class="fa-solid fa-circle-plus" ></span>
               Add Task
            </h5>
          </div>
          <section class="modal-body">
          <form>
          <div class="form-group">
          <label for = "Title" class="ms-2 position-absolute" style="margin-top: -0.60rem"> <span class="h7 small bg-white text-muted px-1">Title</span></label>
          <input type="text" class="form-control" id="title"  placeholder = "Title"> </input>
          </div>
          
          <div class = "form-group">
          <label for = "Description" class="ms-2 position-absolute" style="margin-top: -0.60rem"> <span class="h7 small bg-white text-muted px-1">Description</span></label>
          <input type="text" class="form-control mt-3" id="title" placeholder = "Description"></input>
          </div>
          <div class = "form-group">
          <label for = "Deadline" class="ms-2 position-absolute" style="margin-top: -0.60rem"> <span class="h7 small bg-white text-muted px-1">Deadline</span></label>
          <input type = "date" class = "form-control mt-3" id ="deadline" v-modal = "deadline">
          </div>
          <div class = "form-group">
            <div>Priority: {{priority}} </div>
            <input type="radio" name="priority" id="low" value = "Low" v-modal = "priority" />
            <label for="low" class = "radio"> Low </label>
            <input type="radio" name="priority" id="med" value = "Med" v-modal = "priority"/>
            <label class= "radio" for="med"> Med </label>

            <input type="radio" id="high" value = "High" v-modal = "priority" name="priority"/> 

            <label for="high" class= "radio"> High </label>
            </div>
          

          </section>

          <footer class="modal-footer">
          <div>
            <button type="button" class="btn btn-primary" @click="submitTask">
              <span class="fa-solid fa-circle-plus"></span> Add
            </button>
            <button type="button" class="btn btn-danger" @click="close">
              <span class="fa-solid fa-circle-xmark"></span> Cancel
            </button>
            </div>
          </footer>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.75);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4;
  margin: 1;
}

.modal {
  background: rgba(240, 248, 255, 0.18);
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  background: blue;
  color: white;
  justify-content: center;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
  justify-content: flex-end;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
  margin: 5;
}

.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}
</style>

<script>
export default {
  name: 'Modal',
  props: {
    isModalVisible: Boolean,
    existing_description: String, 
    existing_deadline: String, 
    existing_priority: String, 
    tasks: Array
  }, 
  watch:{
    deadline(){
      if(this.deadline.includes("-")){
        this.deadline = this.formatDate(this.deadline)
      }
    }
  }, 
  methods: {
    submitTask(){
      if(this.$refs.form.validate()){
        this.$emit('submitTask', this.title, this.description, this.deadline, this.priority);
        this.clear(); 
        this.close();
      }
    }, 
    close() {
      this.$emit('close');
    },
    clear(){
      this.title = '';
      this.description = '';
      this.deadline = ''; 
      this.priority = 'low'; 
      this.$refs.form.resetValidation();
    }
  },
    /*getParentData(){
      this.description=this.existing_description;
      this.deadline=this.existing_deadline;
      this.priority=this.existing_priority;
      },
    formatDate(date){
      if (!date) return null;
      const [year, month, day] = date.split('-');
      return `${month}/${day}/${year}`;
    },
    checkValidTitle(title){
      return !this.tasks.filter(e => e.title === title).length > 0
    },*/

  data(){
    return {
      title: '',
      description: '',
      priority: 'low',
      deadline: '', 
      date: '', 
      titleRules: [
        v => !!v || "Title is required",
        v => this.checkValidTitle(v) || 'Title must be unique', 
      ],
    }
  }
};
</script>

