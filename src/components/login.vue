<template>
    <div class="container-fluid bg-dark loginHeight" >
        <div class="container bg-dark mb-3" v-if="!login">
                <div class="input-group" v-if="!login">
                    <input type="text" v-model="username" class="form-control mr-2" placeholder="Enter your username">
                    <input type="password" class="form-control" placeholder="Enter your password"/>
                    <button class="btn btn-warning" @click="checkLogin" type="submit" >Log In</button>
                </div>
        </div>
        <div class="container bg-dark mb-3" v-if="login">
            <div class="row">
                <div class="col-3 h3Text">
                    <h3 class="text-warning">Hello,{{role}}</h3>
                </div>
                <div class="col-auto">
                    <button @click="logout" type="submit" class="btn btn-warning">Log Out</button>
                </div>
            </div>
        </div>
    </div>
    
</template>

<script>


export default {
    name:"Login",
    data() {
        return {
            username:'',
            password:'',
            message:'',
            login: false
        }
    }, beforeMount(){
        if(localStorage.getItem('name')){
            this.login=true
        }
    },
    methods: {
        logout(){
            localStorage.clear()
            this.login = false
            this.$router.push('/')
        },

        checkLogin() {
            this.message = ''
            //check if username password have value
            if (this.username.length==0 || this.password.length==0 ){
                this.message = "Please provide necessary information"
                return
            }

            const jsonBody = JSON.stringify( {
                'user': this.username,
                'pwd': this.password
            })

            fetch('http://47.242.250.90:18888/auth', {
                method:'POST',
                mode: 'cors',
                headers :{
                    'Content-type': 'application/json'
                },
                body:jsonBody,
                role:''
            })
            .then((res,err) => {
                if(err)
                    throw 'communication error'
                if (res.status == 200)
                return res.json ()
                else
                throw "Login Failed"
            })
            .then(json=> {
                this.login=true
                if (json.role == 1){
                    this.role="staff"
                } else {
                    this.role = "......"
                }
                this.username=""
                this.password=""
                localStorage.setItem("name",JSON.stringify(json))
            })
            .catch(err=> {
                if (err) {
                    this.login=false
                    this.message = err
                }
            }
            ) 
        }
    }
}
</script>

<style scoped>

.loginHeight{
    height: 4em;
}

.h3Text{
    text-align: left;
}
</style>
