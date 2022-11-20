<template>
  <div class = "container">
    <h2 class = "text-center mt-5"> FRAMEWORKS </h2>

    <!-- Input -->
    <div class = "d-flex"> 
    <input type = "text" placeholder = "Enter Task" class = "form-control">
    <button class = "btn btn-warning rounded-0"> SUBMIT </button>
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
    <tr>
    <td> Title </td>
    <td> Description </td>
    <td> Deadline </td>
    <td> Priority </td>
    <td> Is Complete </td>

    <td>
    <div class = "text-center">
    <button class = "btn btn-primary btn-sm w-75" > 
    <span class = "fa fa-pen"></span> Update </button>
    </div>
    <div class = "text-center">
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
export default {
  name: 'Todo',
  props: {
    msg: String,
  },

  data(){
    return{
      tasks: 
      {
        Title: 'Title' , 
        Description: 'Description',
        Deadline: 'Deadline',
        Priority: "Priority",
        IsComplete: "Is Complete",
        Action: "Update or Delete"
      }
    }
  }
  
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
