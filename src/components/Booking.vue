<template>
    <div class="Booking">
        <div class="container_Booking">
            <h2>Sign Up</h2>
            <form v-on:submit.prevent="processSignUp" >
                <input type="number" v-model="user.booking.people" placeholder="People">
                <br>
                <input type="date" v-model="user.booking.bookingdate" placeholder="Date and hour">
                <br>-->
                <button type="submit">Send</button>
            </form>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: "Booking",
    data: function(){
        return {
            booking: {
                bookingdate: (new Date()).toJSON().toString(),
                people: "",
            }
        }
    },
    methods: {
        processSignUp: function(){
            axios.post(
                "https://brayans-be.herokuapp.com/bookingCreate/",
                this.booking,
                {headers: {}}
            )
                .then((result) => {
                    let dataSignUp = {
                        username: this.user.username,
                        token_access: result.data.access,
                        token_refresh: result.data.refresh,
                    }
                    this.$emit('completedSignUp', dataSignUp)
                })
                .catch((error) => {
                    console.log(error)
                    alert("ERROR: Fallo en el registro.");
                });
        }
    }
}
</script>

<style>
    .signUp_user{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .container_signUp_user {
        /*border: 3px solid #283747;*/
        border-radius: 10px;
        width: 20%;
        height: 68%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .signUp_user h2{
        color: #283747;
    }

    .signUp_user form{
        width: 80%;
    }

    .signUp_user input{
        height: 40px;
        width: 100%;
        box-sizing: border-box;
        padding: 10px 20px;
        margin: 5px 0;
        border: 1px solid #283747;
    }

    .signUp_user button{
        width: 100%;
        height: 40px;
        color: #E5E7E9;
        background: #283747;
        border: 1px solid #E5E7E9;
        border-radius: 5px;
        padding: 10px 25px;
        margin: 5px 0 25px 0;
    }

    .signUp_user button:hover{
        color: #E5E7E9;
        background: crimson;
        border: 1px solid #283747;
    }   
</style>