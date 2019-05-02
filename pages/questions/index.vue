<template>
  <section class="container">
    <div>
      <h1 class="title">
        musclionaire-app
      </h1>
      <h2 class="subtitle">
        Questions
      </h2>
      <dev v-for="question in questions" :key="question.id">
        <p>{{ question.text }}</p>
        <button>A: {{ question.answers[0] }}</button>
        <button>B: {{ question.answers[1] }}</button>
        <button>C: {{ question.answers[2] }}</button>
        <button>D: {{ question.answers[3] }}</button>
        <p>{{ question.answer }}</p>
      </dev>
    </div>
  </section>
</template>

<script>
import firebase from '~/plugins/firebase.js'

const db = firebase.firestore()
db.settings = { timestampsInSnapshots: true }
// const collection = db.collection('questions')
// console.log(collection.firestore)


export default {
  async asyncData({ params }) {
    return {
      questions: await getAllDocs('questions')
    }
  }
}
// get all documents
async function getAllDocs(collection) {
    const obj = [];
    const colRef = db.collection(collection)
    const allSnapShot = await colRef.get()
    allSnapShot.forEach(doc => {
      obj.push(doc.data())
    })
    console.log(obj)
    return obj
}

</script>

<style>
</style>
