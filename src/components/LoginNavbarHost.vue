<template>
    <div class="header">
        <a class="logo">
            <router-link to="/home">
                <img src="https://drive.google.com/uc?export=view&id=1BkDWEKkJCkMcyIE81ydzIluN134CZxzK" alt="CartaRoom">
            </router-link>
        </a>
        <div class="header-right">
            <router-link to="/home">
                <i class='fas fa-door-open' style="position: relative">&nbsp;&nbsp;&nbsp;&nbsp;</i>
            </router-link>
            <router-link to="/addRoom">
                <i class='fas fa-plus' style="position: relative">&nbsp;&nbsp;&nbsp;&nbsp;</i>
            </router-link>
            <router-link to="/currentBookings">
                <i class="fas fa-concierge-bell" style="position: relative">&nbsp;&nbsp;&nbsp;&nbsp;</i>
            </router-link>
            <router-link to="/allBookings">
                <i class="fas fa-user-clock" style="position: relative">&nbsp;&nbsp;&nbsp;&nbsp;</i>
            </router-link>
            <router-link to="/allCustomers">
                <i class="fas fa-address-book" style="position: relative"></i>&nbsp;&nbsp;&nbsp;&nbsp;
            </router-link>
            <button class="navButtons" @click="logout">LOGOUT</button>
        </div>
    </div>
</template>
<script>
    import firebase from 'firebase';
    export default {
        name: "LoginNavbarHost",
        methods: {
            logout: function () {
                firebase.auth().signOut().then(() => {
                    this.$router.replace('/')
                })
            }
        }
    }
</script>
<style scoped>
    * {
        box-sizing: border-box;
    }
    body {
        margin: 0;
    }
    .header {
        overflow: hidden;
        padding: 20px 10px;
        text-align: left;
    }
    .header a {
        color: black;
        text-align: center;
        padding: 12px;
        text-decoration: none;
        font-size: 18px;
        line-height: 25px;
        border-radius: 4px;
    }
    .header a.logo {
        font-size: 25px;
        font-weight: bold;
    }
    .header a.active {
        background-color: dodgerblue;
        color: white;
    }
    .header-right {
        float: right;
        padding-top: 10px;
        color:#2196F3;
    }
    img {
        width: 20%;
        height: auto;
    }
    .navButtons {
        background: rgba(47, 69, 80, 1);
        border: 1px solid #828282;
        margin-left: 20px;
        height: 35px;
        width: 90px;
        box-sizing: border-box;
        border-radius: 10px;
        color: white;
        font-family: Roboto;
        font-weight: normal;
        font-size: 16px;
        text-align: center;
    }
    @media screen and (max-width: 500px) {
        .header a {
            float: none;
            display: block;
            text-align: left;
        }
        .header-right {
        float: none;
        }
    }
</style>
