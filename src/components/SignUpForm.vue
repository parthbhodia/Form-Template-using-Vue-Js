<template >
    <form @submit.prevent="handleSubmit">
        <label for="">Email:</label>
        <input type="email" required v-model="email">

        <label for="">Password:</label>
        <input type="password" required v-model="password">
        <div v-if="passwordError">{{ passwordError}}</div>

        <label for="">Role</label>
        <select v-model="role">
              <option value="developer">Web developer</option>  
              <option value="designer">Web designer</option>  
        </select>

       
        <!-- <div class="names">
            <input type="checkbox" value="Shaun" v-model="names">
            <label for="">Shaun</label>
        </div>

          <div class="names">
            <input type="checkbox" value="Parth" v-model="names">
            <label for="">Parth</label>
        </div>

          <div class="names">
            <input type="checkbox" value="Hem" v-model="names">
            <label for="">Hem</label>
        </div> -->

        <label for="skill">skills</label>
        <input type="text" v-model="tempSkills" @keyup="addSkills">
        <div v-for="skill in skills" :key="skill" class = "pill">
          <span @click="deleteSkills(skill)">  {{ skill}} </span>
        </div>


         <div class="terms">
            <input type="checkbox" required v-model="terms">
            <label for="">Accept terms and conditions</label>
        </div> 

        <button class="submit" >
            Submit
        </button>

    </form>

    <p>Email: {{email}}</p>
    <p>Role: {{ role}}</p>
    <p>Terms Accepted: {{ terms }}</p>
    <p>Names: {{names }}</p>
</template>
<script>

export default {
    data(){
        return{
            email: "abc@umcb.edu",
            password: "",
            role: "designer",
            terms: false,
            names: [],
            tempSkills: "",
            skills: [],
            passwordError: ""
        }
    },
    methods: {
        addSkills(e) {
            if(e.key === "," && this.tempSkills)
            {
                if (!this.skills.includes(this.tempSkills))
                {
                    this.skills.push(this.tempSkills)
                }
                this.tempSkills = ""
            }

        },
        deleteSkills(skill){
            this.skills = this.skills.filter((item)=> {
                return skill != item
            })

        },

        handleSubmit(){
            //validate error
            this.passwordError = this.password.length > 5 ? '' : 'Password must be atleast 6 chars long'
            
            if(!this.passwordError){
                console.log("Submit Form");
            }
        }
    }
    
}
</script>
<style>
    form {
        max-width: 420px;
        margin: 30px;
        background: #fff;
        text-align: left;
        padding: 40px;
        border-radius: 10px;

    }

    label { 
        color: #aaa;
        display: inline-block;
        margin: 25px 0px 15px;
        font-size: 1 em;
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
        border-bottom: 1px solid #ddd;
        color: #555;
    }

    input[type="checkbox"] { 
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
    }
    
    .pill{
        margin: 2px;
        padding: 5px;
        color: #555;
        display: inline-block;
        border-radius: 5px;
        background: #eee;
        cursor: pointer;
    }

    button {
        margin-top: 20px;
        padding: 10px 20px;
        color: #eee;
        background: blue;
        border: none;
        border-radius: 10px;
    }

    .submit {
        text-align: center;
    }
</style>