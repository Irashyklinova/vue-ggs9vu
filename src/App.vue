<template>
<div id="app">
 <h2>Список пользователей!</h2>
 <div v-if="users.length === 0"><div id="preloader"></div></div>
 <div class="card" v-for="user in users" :key="user.id.value">
 <img class="photo" :src="user.picture.large" alt="photo" />
 <div>
    {{ user.name.title }}.
    {{ user.name.first }}
    {{ user.name.last }}
 </div>
 <div>
   ~{{ user.location.city }}~
 </div>
 <div>
   ~{{ user.dob.age }}~
 </div>
 <div>
   Birthday:
   {{
   new Date(user.registered.date).getDate(user.registered.date) +
   '.' +
   (new Date(user.registered.date).getMonth(user.registered.date) + 1) +
   '.' +
   new Date(user.registered.date).getFullYear(user.registered.date) +
   ' '
   }}
 </div>
 <div>
   ~{{user.gender}}~
 </div>
 <div>
   {{ user.phone }}
 </div>
 <div>
   <br> <a href="#">{{ user.email }}</a> </br>
 </div>
</div>
</template>

<script>

export default {
name: 'App',
components: {},

data(){
return{
users:[],
};
},

mounted(){
fetch('https://randomuser.me/api/?results=10')
.then((response) => {
return response.json();
})
.then((data) => {
console.log(data);
this.users = data.results;
});
},
};
</script>

<style>
#preloader {
position: fixed;

left: 0;
top: 0;
z-index: 999;
width: 100%;
height: 100%;
overflow: visible;
background: #fbfbfb url('https://cdnjs.cloudflare.com/ajax/libs/file-uploader/3.7.0/processing.gif') no-repeat center center;
}


.hidden {
visibility: hidden;
opacity: 0;
transition: visibility 0s 2s, opacity 2s linear;
}
#app {
font-family: Avenir, Helvetica, Arial, sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
text-align: center;
color: #000000;
margin-top: 60px;
display: flex;
flex-direction: column;
flex-wrap: wrap;
width: 1000px;
margin: 0 auto;
align-items: center;

}
.card {
margin-bottom: 20px;
border: 2px solid;
width: 300px;
background-color:#f5f5dc;
}
.photo{
border: 3px solid;
border-radius: 10px;
margin-top: 10px;
}
</style>

