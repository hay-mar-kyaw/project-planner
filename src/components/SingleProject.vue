<template>
    <div class="project" :class="{complete:project.complete}">
        <div class="flexing">
            <div>
                <h3 @click="showDetail= !showDetail">{{ project.title }}</h3>
            </div>
            <div>
                <span class="material-icons" @click="deleteProject">
                    delete
                </span>
                <router-link :to="{name:'editProject',params:{id:project.id}}">
                    <span class="material-icons" >
                        edit
                    </span>
                </router-link>
                
                <span class="material-icons" @click="finishProject">
                    done
                </span>
            </div>
        </div>
        
        
        <p v-if="showDetail">{{ project.detail }}</p>
        {{ project.complete }}
        
    </div>
</template>

<script>
    export default {
        props:['project'],
        data(){
            return{
                showDetail:false,
                api:'http://localhost:3000/projects/'
            }
        },
        methods:{
            deleteProject(){
                let deleteRoute=this.api+this.project.id
                fetch(deleteRoute,{method:"DELETE"})
                .then(()=>{
                    return this.$emit('delete',this.project.id)
                })
                .catch((err)=>{
                    console.log(err.message());
                })
            },
            finishProject(){
                
                let finishRoute=this.api+this.project.id
                fetch(finishRoute,{
                    method:"PATCH",
                    headers:{
                                "Content-Type":"application/json"
                    },
                    body:JSON.stringify(
                        {
                            complete:!this.project.complete
                        }
                    )
                })
                .then(()=>{
                    return this.$emit("finish",this.project.id)
                })
                .catch((err)=>{
                    console.log(err.message());
                })
            }
        },
        
    }
</script>

<style  scoped>
    .project{
        margin: 10px;
        padding: 20px;
        background-color: #f2f2f2;
        border-left: 6px solid crimson;
        border-radius: 8px;    
    }
    h3{
        color:indigo;
        cursor: pointer;
    }
    .flexing{
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    span{
        margin-left: 10px;
    }
    span:hover{
        color: gray;
        cursor: pointer;
    }
    .complete{
        border-left-color: green;
    }
</style>