<template>
  <v-container class="container">
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">Todo list</h1>
        <div style="margin-top: 50px" class="d-inline-flex">
          <input
            style="border: 1px solid"
            v-model="newTodo"
            type="text"
            placeholder="Enter new task..."
            id="input"
          />
          <v-btn @click="addTodo()">ADD </v-btn>
        </div>

        <div v-if="todosArray.length === 0">
          <H3 style="margin-top: 50px"
            >The list is empty, please add some tasks.</H3
          >
        </div>
        <div v-else class="tableBox text-center">
          <table class="table table-bordered mt-10">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Task</th>
                <th scope="col">Done</th>
                <th scope="col" class="">Delete</th>
                <th scope="col" class="text-center">Edit</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-bind:key="todo.index"
                v-for="(todo, index) in todosArray"
                style="font-weight: bold"
              >
                <th>{{ index + 1 }}</th>

                <td
                  v-if="!todosArray[index].isEditing"
                  :class="{ done: todo.completed }"
                >
                  {{ todo.text }}
                </td>

                <td v-else :class="{ done: todo.completed }">
                  <input
                   style="border: 1px solid"
                  v-model="existingTodo"
                          
                    type="text"
                    id="inputEditTodo"
                  value={existingTodo}
                  />
                </td>

                <div>
                  <input 
                    type="checkbox"
                    id="checkbox"
                    v-model="todo.completed"
                  />
                </div>

                <td>
                  <div class="text-center">
                    <v-btn
                      color="#CD5C5C"
                      elevation="10"
                      x-small
                      @click="deleteTodo(index)"
                    >
                      Delete
                      <v-icon>mdi-delete </v-icon>
                    </v-btn>
                  </div>
                </td>

                <td  v-if="todosArray[index].isEditing">
               

                    <v-btn
                      color="#AFEEEE"
                      elevation="10"
                      x-small
                      v-if="todosArray[index].isEditing"
                      @click="editTodo(index)"
                    >  Update
                    
                      <i class="material-icons">create</i>
                    </v-btn>
                
                  </td>
                
                <td  v-else> 
                 
                    <v-btn
                      color="#AFEEEE"
                      elevation="10"
                      x-small
                     
                      @click="changeTodo(index)"
                    >  Edit
                    
                      <i class="material-icons">create</i>
                    </v-btn>
                 
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",

  data() {
    return {
      newTodo: "",
      existingTodo:"",
      isEditing: false,
      todosArray: [
        { text: "Go outside", completed: false, isEditing: false },
        { text: "Go play", completed: false, isEditing: false },
      ],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo !== "")
        this.todosArray.push({
          text: this.newTodo,
          completed: false,
          isEditing: false,
        });
      this.newTodo = "";
    },
    editTodo(index) {
      this.todosArray[index].isEditing = false;
      this.todosArray[index].text=this.existingTodo;
     
     
    },
    deleteTodo(index) {
      this.todosArray.splice(index, 1);
    },
    changeTodo(index) {
      this.todosArray[index].isEditing = true;
    },
  },
};
</script>

<style >
.done {
  text-decoration: line-through;
  color: red;
  background-color: black;
}

.buttons {
  justify-content: space-evenly;
  padding: 15px;
}
.box {
  display: inline-block;
  border: solid;
  padding: 30px;
}

.space-CheckBox {
  margin-left: 10px;
}
.node {
  justify-items: flex-start;
  display: grid;
}
</style>