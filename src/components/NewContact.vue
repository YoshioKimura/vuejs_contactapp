<template>
  <section class="container">
    <h1>add new contact</h1>
    <form @submit.prevent="saveContact">
      <div class="field">
        <label for class="label">first name</label>
        <div class="control">
          <input type="text" class="input" placeholder="first name" v-model="firstname" required />
        </div>
      </div>
      <div class="field">
        <label for class="label">last name</label>
        <div class="control">
          <input type="text" class="input" placeholder="last name" v-model="lastname" required />
        </div>
      </div>
      <div class="field">
        <label for class="label">email</label>
        <div class="control">
          <input type="email" class="input" placeholder="email " v-model="emailaddress" required />
        </div>
      </div>
      <div class="field">
        <label for class="label">phone number</label>
        <div class="control">
          <input type="text" class="input" placeholder="phonenumber " v-model="phonenumber" required />
        </div>
      </div>

      <div class="field">
        <div class="control">
          <button type="submit" class="button is-link">submit</button>
        </div>
      </div>
    </form>
  </section>
</template>

<script>
import db from './firebaseInit'

export default {
  name: 'new-contact',
  data () {
    return {
      firstname: 'null',
      lastname: 'null',
      emailaddress: 'null',
      phonenumber: 'null'
    }
  },
  methods: {
    saveContact () {
      db.collection('contact')
        .add({
          firstname: this.firstname,
          lastname: this.lastname,
          emailaddress: this.emailaddress,
          phonenumber: this.phonenumber,
          slug: this.generateUUID()
        })
        .then(function (docRef) {
          console.log('Document written with ID: ', docRef.id)
        })
        .catch(function (error) {
          console.error('Error adding document: ', error)
        })
    },
    generateUUID () {
      let d = new Date().getTime()
      let uuid = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(
        /[xy]/g,
        function (c) {
          let r = (d + Math.random() * 16) % 16 | 0
          d = Math.floor(d / 16)
          return (c === 'x' ? r : (r & 0x3) | 0x8).toString(16)
        }
      )
      return uuid
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
section {
  height: 100vh;
}
h1 {
  font-size: 30px;
  margin: 30px 0;
}
.input {
  height: 40px;
}
</style>
