<template>
  <div id="app" class="app">
    <div class="header">
      <h1>Los Brayans Restaurant</h1>
      <nav>
        <button v-if="is_auth" v-on:click="loadHome"> Home </button>
        <button v-if="is_auth" > Booking </button>
        <button v-if="is_auth" v-on:click="logOut"> Log Out </button>
        <button v-if="!is_auth" v-on:click="loadLogIn" > Log In </button>
        <button v-if="!is_auth" v-on:click="loadSignUp" > Sign Up </button>
      </nav>
    </div>

    <div class="main-component">
      <router-view
        v-on:completedLogIn="completedLogIn"
        v-on:completedSignUp="completedSignUp"
        v-on:logOut="logOut"
      >
      </router-view>
    </div>

    <div class="footer">
      <h2>2022 Los Brayans Colombian Restaurant</h2>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data: function(){
    return{
      is_auth: false
    }
  },

  components: {
  },
  methods:{
    verifyAuth: function() {
      this.is_auth = localStorage.getItem("isAuth") || false;
      if (this.is_auth == false)
        this.$router.push({ name: "logIn" });
      else
        this.$router.push({ name: "home" });
    },

    loadLogIn: function(){
      this.$router.push({name: "logIn"})
    },

    loadSignUp: function(){
      this.$router.push({name: "signUp"})
    },

    completedLogIn: function(data) {
      localStorage.setItem("isAuth", true);
      localStorage.setItem("username", data.username);
      localStorage.setItem("token_access", data.token_access);
      localStorage.setItem("token_refresh", data.token_refresh);
      alert("Auth Success!");
      this.verifyAuth();
    },

    completedSignUp: function(data) {
      alert("Sign Up success!");
      this.completedLogIn(data);
    },
    loadHome: function(){
      this.$router.push({ name: "home"});
    },
    logOut: function () {
      localStorage.clear();
      alert("Logged out");
      this.verifyAuth();
    },

  },
  created: function(){
    this.verifyAuth()
  }
}
</script>
 
<style>
  body{
    margin:0 0 0 0;
    background-image: url(https://img.freepik.com/foto-gratis/marco-comida-circular-plano-laico_23-2148708223.jpg?w=1060&t=st=1665193973~exp=1665194573~hmac=2413f5f6b84b892044a29da64c44ba8e24deef259f31176f629beae083757fca);
    background-repeat: no-repeat;
    background-position: 50% 50%;
  }
  .header{
    margin:0%;
    padding:0;
    width: 100%;
    height: 10vh;
    min-height: 100px;
    background-color: #283747;
    color:#E5E7E9;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .header h1{
    width: 20%;
    text-align: center;
  }

  .header nav {
    height: 100%;
    width: 20%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    font-size: 20px;
  }

  .header nav button{
    color: #E5E7E9;
    background: #283747;
    border: 1px solid #E5E7E9;
    border-radius: 5px;
    padding: 10px 20px;
  }

  .header nav button:hover{
    color: #283747;
    background: #E5E7E9;
    border: 1px solid #E5E7E9;
  }

  .main-component{
    height: 25vh;
    margin: 15%;
    padding: 0%;
    /*background: #FDFEFE ;*/
  }

  .footer{
    margin: 0;
    padding: 0;
    width: 100%;
    height: 10vh;
    min-height: 80px;
    background-color: #283747;
    color: #E5E7E9;
  }

  .footer h2{
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>