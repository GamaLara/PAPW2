<template>
    <div>
        <h2 style="display:inline-block;"><b>{{name_user}}</b></h2>
        <template v-if="isChangeName">
                <a v-on:click="isChangeName = false" class="bttn-default wow fadeInUp standard btnvue" data-wow-delay="0.8s"><i class="lnr lnr-pencil"></i></a>
            </template>
            <template v-else>
                <input  v-model="user_name" type="text" name="test"> 
                <a v-on:click= "isChangeName = SaveName(user_name)" class="bttn-default wow fadeInUp standard btnvue" data-wow-delay="0.8s"><i class="lnr lnr-pencil"></i> {{ user_name ? "Guardar" : "Cancelar" }}</a>
        </template>
        <h4 class="font-yellow">Key Account Manager</h4> 
        <ul class="information margin-tb-30">
            <li><b class="font-yellow">BORN</b> : Cumpleaños
                <template v-if="isChangeBorn" >
                    <a v-on:click="isChangeBorn = false" class="bttn-default wow fadeInUp standard btnvue" data-wow-delay="0.8s"><i class="lnr lnr-pencil"></i></a>
                </template>
                <template v-else>
                    <input  v-model="user_birthdate" type="date" placeholder="Date" required="" onfocus="(this.type='date')"> 
                    <a v-on:click= "isChangeBorn = SaveBirthdate(user_birthdate)" class="bttn-default wow fadeInUp standard btnvue" data-wow-delay="0.8s"><i class="lnr lnr-pencil"></i> {{ user_birthdate ? "Guardar" : "Cancelar" }}</a>
                </template>
            </li>
            <li><b class="font-yellow">EMAIL</b> : {{email}}</li>
            <li><b class="font-yellow">MARITAL STATUS</b> : Married
                <template v-if="isChangeMartial">
                    <a v-on:click="isChangeMartial = false" class="bttn-default wow fadeInUp standard btnvue" data-wow-delay="0.8s"><i class="lnr lnr-pencil"></i></a>
                </template>
                <template v-else>
                    <input  v-model="user_statusMarital" type="text"> 
                    <a v-on:click= "isChangeMartial = SaveStatusMartial(user_statusMarital)" class="bttn-default wow fadeInUp standard btnvue" data-wow-delay="0.8s"><i class="lnr lnr-pencil"></i> {{ user_statusMarital ? "Guardar" : "Cancelar" }}</a>
                </template>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        props: {
            id_user:Number,
            name_user:String,
            email:String,
        },
        data() {
            return { 
               isChangeName: true,
               isChangeBorn: true,
               isChangeMartial: true,
               user_name: "",
               user_birthdate: "",
               user_statusMarital: "",
               name:"",
               born:"",
               marital:""
            }
        },
        mounted() {
            console.log('Component mounted.');      
        },
        methods: {
            SaveName: function() {
                axios.post('/profile/editname', {
                    name: this.user_name,
                    user: this.email,
                })
                .then(function (response) {
                    console.log(response);
                    return true;
                })
                .catch(function (error) {
                    console.log(error);
                });
            },
            SaveBirthdate: function() {
                axios.post('/profile/editbirthdate', {
                    name: this.user_birthdate,
                    user: this.email,
                })
                .then(function (response) {
                    console.log(response);
                })
                .catch(function (error) {
                    console.log(error);
                });
            },
            SaveStatusMarital: function() {
                axios.post('/profile/editstatusmarital', {
                    name: this.user_statusMarital,
                    user: this.email,
                })
                .then(function (response) {
                    console.log(response);
                })
                .catch(function (error) {
                    console.log(error);
                });
            }
        }
    }
</script>


<style>
.btnvue{
    background-color:#cacaca; 
    border-radius:5px;
}
.standard{
    line-height: 1; 
    float: center;
    font-size: 22px;
    padding: auto;
    margin: auto;
}
</style>