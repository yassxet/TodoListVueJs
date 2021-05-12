<template>
  <v-container class="space-evenly">
    <v-row class="text-center">
      <v-col class="mb-4">
        
        <div class= "container">
        <h1 class="display-2 font-weight-bold mb-3">
          Todo list 
        </h1> 
       
      <input v-model="newTodo" type="text" placeholder="Enter new task..." id="input" >
        <v-btn @click="addTodo()">ADD </v-btn>

<div class="container">
        <ol>
         
            
          <li v-bind:key="todo.index" v-for="(todo,index) in todosArray" style="font-weight: bold;"> 
             <input type="checkbox" id="checkbox" v-model="todo.completed"> 
                <span :class="{done: todo.completed}">{{todo.text}}</span> 
                    
                    <v-btn left
                    color="red"
                    elevation="10"
                    small
                    class="deleteBtn" @click="deleteTodo(index)"> Delete
                    <v-icon   right>mdi-delete </v-icon>

                    </v-btn>
                    

                   <v-btn right
                    color="blue"
                    elevation="10"
                    small
                    class="editBtn " @click="editTodo(index)"> Edit
                     <i class="material-icons" >create</i>
                     </v-btn>
                   
                 
                 
                  
          </li>
            
         
       

        </ol>
       </div>
       
       
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data(){
      return{
              newTodo:'',
              todosArray:[
              {text:'Go shopping',completed:false},
              {text:'Go play', completed:false}]
              
      }
    } ,
    methods:{
        addTodo(){
          if(this.newTodo!=='')
           this.todosArray.push({text:this.newTodo,completed:false}) 
           this.newTodo=''
        },
        editTodo(){
        //  this.todosArray.index

        },
        deleteTodo(index){
          this.todosArray.splice(index,1)
        }
    }  
 }
</script>

<style >
.done{
  text-decoration: line-through;
  background-color: rgb(118, 226, 118);
}
.container{
  text-align: center;

  padding: 30px;
  margin: 50;
 justify-content: space-evenly;
}

</style>