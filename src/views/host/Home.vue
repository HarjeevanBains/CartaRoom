<template>
    <div class="home">
        <div class="banner">
            <p class="banner_text">All Your Rooms</p>
        </div>

        <div class="rooms" v-for="room of rooms.slice().reverse()" v-bind:key ="room['.key']">
            <div class="row">
                <div class="column1">
                    <img src="../../assets/banner/roomView/room1.jpg">
                </div>
                <div class="column2">
                    <div class="rowA">
                        <div class="column1A">
                            <label>Room Name</label>
                        </div>
                        <div class="column2A">
                            <p class="info">{{ room.name }}</p>
                        </div>
                    </div>

                    <div class="rowA">
                        <div class="column1A">
                            <label>Capacity</label>
                        </div>
                        <div class="column2A">
                            <p class="info">{{ room.capacity }}</p>
                        </div>
                    </div>

                    <div class="rowA">
                        <div class="column1A">
                            <label>Business Address</label>
                        </div>
                        <div class="column2A">
                            <p class="info">{{ room.address }}</p>
                        </div>
                    </div>

                    <div class="rowA">
                        <div class="columnButtons">
                            <button v-on:click="viewRoom(room.roomID)">View</button>
                        </div>
                    </div>
                </div>
            </div>
<!--            -->
        </div>
    </div>
</template>
<script>
    import firebase from 'firebase';
    import db from '@/firebase.js';

    var userID;
    firebase.auth().onAuthStateChanged(function (user) {

        if (user) {
            // console.log(user.uid); //a@a.com = gbEw7s5ic1drxG3vgFWD3DAMb972
            userID = user.uid;
        } else {
            // console.log("No user available");
            userID = "null";
        }
    });

    export default {
        name: 'home',
        data() {
            return {
                rooms: []
            }
        },
        created() {
            db.ref('rooms').orderByChild("hostID").equalTo(userID).once('value').then((snapshot) => {
                this.rooms = [];
                snapshot.forEach((doc) => {
                    this.rooms.push(doc.val());
                })
            }).catch((error) => {
                console.log(error);
            });
        },
        methods: {
            viewRoom: function (id) {
                this.$router.push({
                    name: 'RoomViewHost',
                    params: {
                        id: id
                    }
                })
            }
        }
    }

</script>
<style scoped>
    .column1 {
        width:30%;
    }

    .column1A {
        width:60%;
    }

    .column1A label{
        float: right;
        padding-right: 10%;
    }

    .column2 {
        width:80%;
     }

    .column2A {
        width:40%;
        float: right;
    }

    .row {
        margin:auto;
        width: 90%;
        display:flex;
        align-items:center;
    }

    .rowA {
        display:flex;
        align-items:center;
    }

    img{
        width: 100%;
        height:auto;
    }
    .banner_text {
        font-family: Rajdhani;
        font-style: normal;
        font-weight: 600;
        font-size: 90px;
        line-height: 191px;
        text-align: center;
        color: #000000;
    }
    .banner {
        height: 400px;
        width: 100%;
        background: linear-gradient(rgba(255,255,255,.5), rgba(255,255,255,.5)),url("../../assets/banner/Host2.jpg");
        background-repeat: no-repeat;
        background-size: cover;
        margin-top:-150px;
        padding-top:150px;
    }
    label {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        font-style: normal;
        font-weight: normal;
        font-size: 25px;
    }
    .rooms{
        margin-left: auto;
        margin-right: auto;
        padding-top: 1%;
        padding-bottom: 1%;
        margin-top: 45px;
        margin-bottom: 65px;
        background: rgba(218, 229, 227, 0.9);
        border-radius: 15px;
        width: 50%;
    }

    .info{
        border: 0.75px solid darkgrey;
        width: 100%;
        font-size: 20px;
        line-height: 35px;
        box-sizing: border-box;
        background: #FFFFFF;
        border-radius: 5px;
        margin-top:10px;
        margin-bottom:10px;
    }
    .columnButtons{
        width:100%;
        margin-top:10px;
    }
    .columnButtons button {
        display:block;
        margin:0 auto;
        cursor: pointer;
        background: #FFFFFF;
        border-radius: 15px;
        height: 44px;
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        font-style: normal;
        font-weight: bold;
        font-size: 18px;
        line-height: 35px;
        text-align: center;
        width: 25%;
        color: #000000;
    }
</style>
