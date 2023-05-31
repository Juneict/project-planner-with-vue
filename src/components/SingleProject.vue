<template>
    <div class="projects" :class="{completed:project.complete}">
        <div class="job-container">
            <div>
                <h3 @click="showDetail = !showDetail">{{  project.title }}</h3>
                <p v-if="showDetail">{{ project.detail }}</p>
            </div>
            <div>
                <span class="icons" @click="deleteProject">
                    <i class="fa-solid fa-trash"></i>
                </span>
                <router-link :to="{name:'EditProject',params:{id:project.id}}">
                    <span class="icons">
                        <i class="fa-solid fa-pencil"></i>
                    </span>
                </router-link>
                <span class="icons" @click="completeProject">
                    <i class="fa-solid fa-check"></i>
                </span>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    props:[
        'project'
    ],
    data(){
        return {
            showDetail : false,
            api : "http://localhost:3000/projects/"
        }
    },
    methods:{
        deleteProject(){
            let deleteRoute = this.api+this.project.id;
            fetch(deleteRoute, { method: 'DELETE' })
            .then(()=>{
                this.$emit('delete', this.project.id)
            })
            .catch((err)=>{
                console.log(err);
            })
        },
        completeProject(){
            let completeUpdateRoute = this.api+this.project.id;
            fetch(completeUpdateRoute, {
                 method: 'PATCH',
                 headers:{
                    "Content-Type":"application/json"
                 },
                 body:JSON.stringify({
                    complete:!this.project.complete
                 })
            })
            .then(()=>{
                this.$emit('complete', this.project.id)
            })
            .catch((err)=>{
                console.log(err);
            })
        }
    }
}
</script>

<style>
    .projects{
        padding: 20px;
        background-color: #f2f2f2;
        margin: 10px;
        border-left: 6px solid crimson;
        border-radius: 8px  ;
    }
    h3{
        color: indigo;
        cursor: pointer;
    }
    .job-container{
        display: flex;
        justify-content: space-between;
        align-items:center;
    }
    .icons{
        margin: 10px;
        cursor: pointer;
    }
    .icons:hover{
        color: #777;
    }
    .completed{
        border-left-color: green;
    }
</style>