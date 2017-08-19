<template>
  <div id="app" class = "container">

  <div class = "page-header">
      <div>
        <img src= "./assets/logofa.png" height="80" width="80">
        <h3> Welcome to Fast-ask-community</h3>
      </div>
 </div>
  <div class="panel panel-default">
    <div class="panel-heading">
      <h4>Live chat</h4>
    </div>
    <div class="panel-body">
     <div class="table table-striped">
       <thead></thead>
       <tbody>
         <div id="body">
           <tr v-for = "send in message">
           <td> {{send.name}}  </td><td> <p>:</p> </td><td>  {{send.text}} </td>
            <td> <button class="glyphicon glyphicon-trash" v-on:click="removeMessage(send)"></button></td>
           </tr>
         </div>

       </tbody>
     </div>
    </div>
  </div>

  <div class="panel panel-default">

    <form id="form" class="form-inline" v-on:submit.prevent="send">
      <div class="form-group">
        <label for="whosend">name :</label>
        <input type="text" id ="whosend" class="form-control" v-model="newmessage.name">
      </div>
      <div class="form-group">
        <label for="textsend">message :</label>
        <input type="text" id ="textsend" class="form-control" v-model="newmessage.text">
      </div>
      <input type="submit" class="btn btn-primary" value="send">
    </form>
  </div>

</div>


</template>

<script>
import Hello from '@/components/Hello'
import Firebase from 'firebase'
let config ={
   apiKey: "AIzaSyAhezqZkZPalZCdLgO9k5HhsCGiIY9MUQI",
   authDomain: "my1stfirebaseproject-5a142.firebaseapp.com",
   databaseURL: "https://my1stfirebaseproject-5a142.firebaseio.com",
   projectId: "my1stfirebaseproject-5a142",
   storageBucket: "my1stfirebaseproject-5a142.appspot.com",
   messagingSenderId: "569992906836"
}
let app = Firebase.initializeApp(config);
let db = app.database();
let messageSaid = db.ref('message');

export default {
  name : 'app',
  firebase: {
  message : messageSaid
  },
  data(){
    return{
      newmessage : {
        name :'',
        text :''
      }
    }
  },
  methods : {
    send :function() {
      messageSaid.push(this.newmessage)
      this.newMessage.name='';
      this.newMessage.text='';
      toastr.success("Send completed")
    },
    removeMessage :function(send) {
      messageSaid.child(send['.key']).remove();
      toastr.success("Delete completed")
    }
  }
}
</script>

<style>
 #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
  margin-top: 60px;
}
#body{}
#inputmessage{

}
</style>
