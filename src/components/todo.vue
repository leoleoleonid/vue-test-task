<template >
    <div class="todo" v-on:keyup.13="addTask">
        <h1 class="title">Checklist</h1>

        
         <ui-tabs type="text">
            <ui-tab title="Pending">
                <ul class="tasks" v-bind:class="{Long:  pendingLength}">
                    <li v-for="task in tasks"   :class="{complete : task.complete}">   
                        <label v-if="!task.complete" class="list" v-on:click="remove(task.id,1)" >
                            <ui-checkbox v-model="task.complete"    />
                            {{task.name}}
                        </label>
                    </li>
                </ul>
            </ui-tab>


            <ui-tab title="Complete">
                <ul class="tasks" v-bind:class="{Long:  compliteLength}">
                    <li v-for="task in tasks"   :class="{complete : task.complete}">
                        <label v-if="task.complete" class="list" v-on:click="remove(task.id,0)" >
                            <ui-checkbox v-model="task.complete"    />
                            {{task.name}}
                        </label>
                    </li>
                </ul>
            </ui-tab>

        </ui-tabs>

        <div class="flor">
            <ui-textbox placeholder="e.g. 'read vue.js guide'" v-model="newTaskName"></ui-textbox>
            <ui-button color="primary" @click="addTask"  icon="add">Add</ui-button>
        </div>

        
    </div>
</template>


<script>
    export default {
        data () {
            return {
                newTaskName : '',
                tasksLength : false,
                tasks : [
                    {id : 1,name : 'create skeleton of todo', complete : true},
                    {id : 2,name : 'add ability to add tasks', complete : true},
                    {id : 3,name : 'clear task name after clicking "Add"', complete : false},
                    {id : 4,name : 'put "Add" button in one line with input', complete : false},
                    {id : 5,name : 'add new task by hitting Enter instead of clicking "Add"', complete : false},
                    {id : 6,name : 'replace <input> with <ui-checkbox> in tasks list', complete : false},
                    {id : 7,name : 'when task is complete cross it out', complete : false},
                    {id : 8,name : 'split tasks into "pending" and "complete" tabs using keen-ui component <ui-tabs>', complete : false},
                    {id : 9,name : 'don\'t allow to add empty tasks', complete : false},
                    {id : 10,name : 'make list of tasks scrollable, if there\'re are a lot of tasks', complete : false},
                    {id : 11,name : 'extract list item into a separate vue.js component', complete : false},
                    {id : 12,name : 'persist tasks list in a local storage', complete : false},
                    {id : 13,name : 'add animation on task completion', complete : false}
                ]
            }
        },

        methods : {
            addTask () {
                if (this.newTaskName) this.tasks.push({ id : Date.now() ,name : this.newTaskName, complete : false});
                this.newTaskName = '';
                this.chechLength();
                // console.log(this.tasks.length);
                // this.remove();  
            },
            remove (id,fromPending) {
                if(fromPending){
                    this.tasks.forEach((item,i,arr)=> {
                      if (item.id == id) this.tasks[i].complete = true;
                    });
                }else{
                    this.tasks.forEach((item,i,arr)=> {
                      if (item.id == id) this.tasks[i].complete = false;
                    });     
                }
                this.chechLength();                
            },
            chechLength (){
                let  counterPending= this.tasks.filter((item)=> {
                  return !item.complete ;
                }).length;
                let counterComplite = this.tasks.filter((item)=> {
                  return item.complete ;
                }).length;
                console.log(counterComplite);
                if(counterComplite > 7) {
                    this.compliteLength = true; 
                }else{
                    this.compliteLength = false; 
                }
                console.log(counterPending);
                if(counterPending > 7) {
                    this.pendingLength = true; 
                }else{
                    this.pendingLength = false; 
                }
            }
        },
        components: {

        }
    };
</script>

<style scoped lang="scss">
    .todo {
        margin: auto;
        background: #fff;
        padding: 20px;
        border-radius: 5px;
        box-shadow: rgba(0, 0, 0, 0.3) 3px 3px 15px;

        .title {
            margin-top: 0;
        }

        .tasks {
            list-style: none;
            padding: 0;
        }
        .Long{
            list-style: none;
            padding: 0;
            overflow:scroll;
            height:250px;
        }
        .flor {
            display: flex;
        }
        .list {
            display: flex;
        }
    }
</style>
