<template>
  <div class="questions-list">
    <div v-for="(question, index) in questions" v-bind:key="index">
      <PostContent v-bind:docID="question.docID" />
    </div>
  </div>
</template>

<script>
import {db} from '../../plugins/firebase'
import PostContent from './PostContent'
export default {
  name: "QuestionsList",
  components: {
    PostContent
  },
  data: function() {
    return {
      questions: [],
    }
  },
  mounted: function(){
    //マウント時に投稿一覧を取得する
    var ref = db.collection('Questions').orderBy('time', 'desc')
      ref.get()
        .then(snapshot => {
          if (snapshot.empty) {
            console.log('No matching documents.');
            return;
          }
          snapshot.forEach(doc => {
            //documentIDを配列で保持する
            var questionData = {
              docID: doc.id
            }
            this.questions.push(questionData)
          });
        })
        .catch(err => {
          console.log('Error getting documents', err);
        });
  },
}
</script>

<style scoped>
.questions-list{
  background-color: #FFFFFF;
}
</style>