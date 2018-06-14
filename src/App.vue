<template>
  <div id="app" class="jumbotron">
    <!-- <img src="./assets/logo.png"> -->
    <div class="container">
      <h1>Hello! Nice to meet you!</h1>
      <hr/>
      <form @submit="addMessage">
        <div class="form-group">
          <input class="form-control"
          v-model="newMessage.title" maxlength="40" autofocus placeholder="Please introduce yourself :)" />
        </div>
        <div class="form-group">
          <textarea class="form-control" 
          v-model="newMessage.text" placeholder="Leave your message here!" rows="3" ></textarea>
        </div>
        <div class="form-group">
          <button class="btn btn-info" type="submit">Send</button>
        </div>
      </form>
      <hr/>
      <div class="card-columns">
        <card :message="firstMessage"></card>
        <card  v-for='(message, index) in messages' :key='index' 
        :message='message'>
        </card>
      </div>
    <!-- <router-view/> -->
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase';
import Card from './components/Card';
// Initialize Firebase
var config = {
  apiKey: 'AIzaSyClw7hywxxvsEj14WGGx-z9SlgJ3f8j5tQ',
  authDomain: 'pleaseintroduceyourself-dc4ea.firebaseapp.com',
  databaseURL: 'https://pleaseintroduceyourself-dc4ea.firebaseio.com',
  projectId: 'pleaseintroduceyourself-dc4ea',
  storageBucket: 'pleaseintroduceyourself-dc4ea.appspot.com',
  messagingSenderId: '594659782946'
};
let app = Firebase.initializeApp(config);
let db = app.database();
let messageRef = db.ref('message');
export default {
  name: 'App',
  data () {
    return {
      firstMessage: {
        isFirst: true,
        title: 'Hello I am Olga',
        text: 'This is first message.',
        timestamp: Date.now()
      },
      newMessage: {
        title: '',
        text: '',
        timestamp: null
      }
    };
  },
  methods: {
    addMessage (e) {
      e.preventDefault();
      if (this.newMessage.title === '') return;
      this.newMessage.timestamp = Date.now();
      messageRef.push(this.newMessage);
      this.newMessage.text = '';
      this.newMessage.title = '';
      this.newMessage.timestamp = null;
    }
  },
  components: {
    Card
  },
  firebase: {
    messages: messageRef
  }

};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.form-group:last-child {
  text-align: left;
}
</style>
