<template>
  <div id="header-container">
    <b-container class="header" v-if="!loading">
      <div class="icon-container" v-on:click="toHomePage">
        <div>
          <img src="../assets/name_it_icon.png" alt="name_it icon" class="name-it-icon">
        </div>
        <div class="name-it-title">name_it</div>
      </div>
      <!-- 投稿ボタン -->
      <b-button variant="light" class="post-button" @click="toPostPage">
        <img src="../assets/post-icon-24px.svg" alt="post-icon">
        投稿
      </b-button>
      <!-- ユーザー情報のコンテナ -->
      <div id="user-container">
        <!-- ログインボタン -->
        <b-button v-on:click="login" v-if="!isUserExist" variant="light" >
          <img src="../assets/login-icon-24px.svg" alt="login-icon"> login
        </b-button>
        <!-- ユーザー名 -->
        <div v-if="isUserExist" v-on:click="toProfilePage" id="user-text-container">
          <div id="user-name-text"> {{ userName }} </div>
        </div> 
        <!-- ログアウトボタン -->
        <b-button v-on:click="logout" variant="light" >
          logout
        </b-button>
      </div>
    </b-container>
  </div>
</template>

<script>
import firebase from 'firebase/app';
import 'firebase/auth'
import {db} from '../plugins/firebase'
export default {
  name: 'CustomHeader',
  data() {
    return {
      isUserExist: false,
      userName: "",
      userID: "",
      currentuser: firebase.auth().currentUser,
      loading: true,
    }
  },
  mounted: function(){
    // userのステータスが変わったとき（ログイン，ログアウト時）にconfirmLoginを実行する
    firebase.auth().onAuthStateChanged(this.confirmLogin);
  },
  methods:{
    login: function(){
      console.log("login")
      var provider = new firebase.auth.GithubAuthProvider();
      firebase.auth().signInWithPopup(provider).then((result) => {
        // ログイン成功
        var user = result.user;
        this.isUserExist = true
        var createAt = result.additionalUserInfo.profile.created_at
        this.userName = result.additionalUserInfo.profile.login
        user.updateProfile({
          displayName: this.userName
        })
        this.initializeUserdb(user, createAt)
        var now = new Date()
        var milliDiffTime = now.getTime() - new Date(createAt).getTime()
        var diffYear = Math.floor(milliDiffTime / 1000 / 60 / 60 / 24 / 365)
        this.$store.dispatch('updatePeriodOfGitHub', diffYear)
        //ページリロード
        // console.log(this.$route.name)
        this.$router.go({ name: this.$route.name })
      }).catch(function() {
        // ログイン失敗
      });
    },
    //デバッグ用のサインアウトメソッド
    logout: function(){
      var router = this.$router
      firebase.auth().signOut()
      .then(function() {
        // Sign-out successful.
        console.log("サインアウト")
        router.push({ name: "HomePage" }, () => {} );
      }).catch(function(error) {
        // An error happened.
        console.log("サインアウトエラー")
        console.log(error.message)
      });
    },
    confirmLogin: function(user){
      // ユーザがログイン状態か確認する
      if (user) {
        console.log("ログイン済み "+ user.displayName)
        this.isUserExist = true
        this.userName = user.displayName
        this.userID = user.uid
        //storeに値をuserIDを保存
        this.$store.dispatch('updateUserID', user.uid)
        this.$store.dispatch('updateUserName', user.displayName)
      } else {
        console.log("未ログイン")
        this.isUserExist = false
      }
      // ログイン確認終了
      this.loading = false
    },
    initializeUserdb: function(user, createAt){
      console.log("DBの初期化  "+ user.uid)
      db.collection("Users").doc(user.uid).set({
        name: this.userName,
        createAt: new Date(createAt)
      })
      .then(function() {
          console.log("Document successfully written!");
      })
      .catch(function(error) {
          console.error("Error writing document: ", error);
      });
    },
    toPostPage: function(){
      if(this.isUserExist){
        this.$router.push({name: 'PostPage'});
      } else {
        alert("投稿するにはログインしてください")
      }
    },
    toHomePage: function(){
      if(this.$route.path == "/"){
        // ページリロード
        // this.$router.go({ name: 'HomePage' })
      } else{
        this.$router.push({name: 'HomePage'});
      }
    },
    toProfilePage: function(){
      if(this.$route.path == "/profile"){
        // ページリロード
        // this.$router.go({ name: 'ProfilePage' })
      } else{
        console.log(this.userID)
        this.$router.push({name: 'ProfilePage', params: {userID: this.userID}});
      }
    },
  },
}
</script>

<style scoped>
#header-container {
  position: fixed;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 70px;
  background-color: #2d3047;
  color: #ffffff;
}

.header {
  display: flex;
  justify-content: flex-start;
  height: 70px;
  padding-top: 5px;
  padding-bottom: 5px;
}

.icon-container {
  margin-right: auto;
  display: flex;
}

.icon-container :hover{
  cursor: pointer;
}

.name-it-icon{
  width: 60px;
}

.name-it-title {
  height: 100%;
  font-size: 30px;
  font-weight: bold;
  padding-left: 10px;
  padding-top: 5px;
}

.post-button{
  width: 100px;
  height: 50px;
  margin-top: 5px;
  margin-bottom: 5px;
}

#user-container {
  width: 200px;
  margin-top: 5px;
  margin-bottom: 5px;
  display: flex;
  justify-content: flex-end;
}

#user-container > * {
  margin-left: 10px;
}

#user-text-container{
  cursor: pointer;
}

#user-name-text{
  /* テキストの高さ揃え */
  padding-top: 9px;

  width: 100px;
  text-align: center;
  font-size: 1.2rem;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
</style>