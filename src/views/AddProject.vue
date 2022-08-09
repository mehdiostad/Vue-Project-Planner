<template>
  <form @submit.prevent="handleSubmit">
    <label >Title:</label>
    <input type="text" required v-model="title">
    <label >Details:</label>
    <textarea v-model="details"></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
data(){
    return{
        datails:'',
        title:'',
    }
},
methods:
{
    handleSubmit(){
        let project = {
            title: this.title,
            detail: this.details,
            compelete: false
        }
        fetch('http://localhost:3000/projects' , {
            method: 'POST',
            headers:{'Content-Type': 'application/json'},
            body:JSON.stringify(project)

        }).then(()=>{this.$router.push('/')}).catch(err=>console.log(err.message))
    }
}
}
</script>

<style>
form{
    background: white;
    padding: 20px;
    border-radius: 10px;
}
label{
    font-weight: bold;
    color: #b7b7b7;
    display: block;
    margin: 20px 0px 10px 0px;
    text-align: left;
    text-transform: uppercase;
    letter-spacing: 1px;
}
input{
    width: 100%;
    padding: 10px;
    border: 0px;
    border-bottom: 1px solid #ddd;
    box-sizing: border-box;
}
textarea{
    width: 100%;
    padding-bottom: 70px;
    border: 1px solid #ddd;
}
form button{
    margin:20px auto 0px;
    padding: 12px;
    background: rgb(0, 198, 0);
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    display: block;
}
</style>