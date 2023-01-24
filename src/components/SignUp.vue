<template>
  <form @submit.prevent="submit">
    <label for="">Email</label>
    <input type="email" v-model="email" required>

    <label for="">Password</label>
    <input type="password" v-model="password">
    <p v-if="errorMsg" class="error">{{errorMsg}}</p>

    <label for="">roles</label>
    <select name="" id="" v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>    

    <div>
        <input type="checkbox" class="check" v-model="accept" required>
        <label for="">Accept Terms and Conditions</label>
    </div>  

    <div class="align">
        <button >Create Account</button>
    </div>

    <!-- multiple checkbox -->
    <label for="">Check Names</label>

    <div>
        <input type="checkbox" class="check" value="Bryan" v-model="name">
        <label for="">Bryan</label>
    </div>
    <div>
        <input type="checkbox" class="check" value="Chaw" v-model="name">
        <label for="">Chaw</label>
    </div>
    <div>
        <input type="checkbox" class="check" value="Khin" v-model="name">
        <label for="">Khin</label>
    </div>

    <div>
        <label for="">Skills</label>
        <input type="text" @keyup="addSkill" v-model="skill">
    </div>
    <div v-for="skill in skills" :key="skill">
        <p>{{skill}} <span @click="deleteSkill(skill)">&#10060;</span></p>
    </div>
  </form>


  


</template>

<script>
export default {
    data() {
        return {
            email: "",
            password: "",
            role:"",
            accept:false,
            name: [],
            skill: "",
            skills: [],
            errorMsg: ""
        }
    },
    methods:{
        addSkill(e) {
            if(e.key === "," && this.skill) {
                this.skills.push(this.skill);
                this.skill = "";
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter(loopskill => {
                // console.log(skill);
                return loopskill !=skill;
            })
        },
        submit() {
            // validation
            console.log("submitted");
            if(this.password.length < 8 ) {
                this.errorMsg="Password must be at least 8 characters"
            }
        }
    }

}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6rem;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 2px solid rgb(192, 192, 192);
        color: #555;
    }
    .check {
        display: inline-block;
        width: 16px;
        position: relative;
        margin: 0 10px 0 0 ;
        top: 2px;
    }
    span {
        cursor: pointer;
        margin-left: 10px;
    }

    button {
        background: royalblue;
        padding: 8px;
        color:white;
        border-radius: 10px;
        border: none;
        text-align: center;
        cursor: pointer;
    }

    .align {
        text-align: center;
    }

    .error{
        color: crimson;
    }
</style>
