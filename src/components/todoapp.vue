<template>

<div>
    <h2 >MY TDOD LIST</h2>
    <div class="d-flex mt-5 ">
        <input type="text" v-model="task"  placeholder="enter task to do"   class="w-100 from control">
        <button v-on:click="submitTask()">submit</button>
        
    </div>
    <table class="table table-bordered">
    <thead>
        <tr>
        <th scope="col">Task</th>
        <th scope="col">Status</th>
        <th scope="col">EDIT</th>
        <th scope="col">DELETE</th>
        </tr>
        <tr  v-for="(task,index) in tasks" :key = "index" >
            <td  :class ="{'line-through' : tasks.status === 'finished'}">
                <span  :class ="{'line-through' : tasks.status === 'finished'}">
                    {{ task.name }}
                </span>
             </td>
            <td>
                <span  
                @click="changeStatus(index)"
                :class ="{
                    'text-center':tasks.status==='to-do',
                    'text-success':tasks.status==='to-do',
                    'text-warning':tasks.status==='to-do', 

                }"
                >
                {{ task.status }}
                </span>
            </td>
            <td>
                <div>
                    <button class="fa fa pen9"   @click="editTask(index)">
                        EDIT
                    </button>
                </div>
               

            </td>
            <td> 
                <div>
                    <button class="fa fa pen9"    @click="deleteTask(index)">
                        DELETE
                    </button>
                </div>
            </td>
        </tr>
    </thead>
    
    </table>
</div>

</template>



<script>
export default{

    name: 'todoapp',
    components : {

    },
    props : {
        msg : String,
    },  
    data(){
        return{
            task : "",
            editedTask : null,
            Status : [ "to-do","in-progress","finished"],
            tasks : [
                {
                    name : "task 1",
                    status: "to-do",
                },
                {
                    name : "task 2",
                    status: "in-progress",
                },
                {
                    name : "task 3",
                    status: "finished",
                },
            ]



        }
    },
    methods: {
        captitalizedFirstCharacter(str)
        {
            return str.chartAt(0).toUppercase()+str.slice(1)
        },

        changeStatus(index)
        {
            let newindex = this.Status.indexOf(this.tasks[index].status);
            if(++newindex>2)
            {
                newindex=0;
                this.tasks[index].status=this.status[newindex];
            }
        },

        editTask(index){
                this.task=this.tasks[index].name;
                this.editTask=index;
        },
        deleteTask(index){
            this.tasks.splice(index,1)
        },
        submitTask()
        {         
            // alert("hello");
            if(this.task.length===0) return ;
            if(this.editedTask != null){
                this.task[this.editedTask].name=this.task;
                this.editedTask=null;
            }
            else{
                this.tasks.push({
                    name :this.task,
                    status:"todo",
                });
            }
            this.task="";
        }

    },
}
</script>