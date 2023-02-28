<template>
  <div>
    <form action="" @submit="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="Password" required v-model="password">
    <div v-if="passwordErorr" class="error" > {{ passwordErorr }}</div>
   
    <label> Role</label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>

    <label >Skills:</label>
    <input type="text"  v-model="tempSkill" @keyup="addSkill">
    <div @click="deleteSkill(skill)" v-for="skill in skills" :key="skill" class="pill" >
        <div >{{ skill }}</div>
    </div>
    

    <div class="terms">
        <input type="checkbox" required v-model="terms">
        <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
        <button>Create An Account</button>
    </div>

  </form>
  <div v-if="showDetail" class="showDetail">
    <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms Accepted: {{ terms }}</p>
  <p>tempSkills: {{ tempSkill }}</p>
  <p>skills:{{ skills }}</p>
  </div>
  </div>
  
</template>

<script>
export default {
    data(){
        return{
            email:"",
            password:"",
            role:"",
            terms:false,
            tempSkill:'',
            skills:[],
            passwordErorr:'',
            showDetail:false,
        }
    },
    methods:{
        addSkill(e){
            console.log(e);
            if(e.key === ',' && this.tempSkill){
                if(this.skills.includes(this.tempSkill)){

                }else{

                    this.skills.push(this.tempSkill)
                }
                this.tempSkill=''
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item)=> skill !==item);
        },
        handleSubmit(e){
            e.preventDefault();
            console.log("form submitted")
            // vallid password'
            this.passwordErorr = this.password.length>5 ? '': 'Password must be at least 6 char long'
            if(!this.passwordErorr){
                this.showDetail = true;
            }
            
            
        }
    }
}
</script>

<style>
    form{
        max-width:420px;
        margin:30px auto;
        background : rgb(167, 158, 158);
        text-align:left;
        padding : 40px ;
        border: radius 10px;

    }
    label{
        color:#262626;
        display:inline-block;
        margin:25px 0 15px;
        font-size:0.6em;
        text-transform: uppercase;
        letter-spacing :1px;
        font-weight:bold;
    }

    input, select{
        display:block;
        padding:10px 6px;
        width:100%;
        box-sizing: border-box;
        border:none;
        border-bottom:1px solid  #7e7e7e;
        color: #343434;
    }
    input[type="checkbox"]{
        display: inline-block;
        width:16px;
        margin:0 10px 0 0;
        position: relative ;
        top : 2px ;
    }
    .pill{
        display:inline-block; 
        margin:20px 10px 0 0;
        padding : 6px  12px ;
        background: #eee;
        border-radius: 20px ;
        font-size:12px ;
        letter-spacing: 1px;
        font-weight: bold;
        color:#777;
        cursor:pointer;

    }
    button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
    }
    .submit {
        text-align: center;
    }
    
</style>