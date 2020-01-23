<template>
  <div class="hello">
    <div v-for="(user, index) in users" :key="index">
      {{ index + 1 }}<input type="text" v-model="user.name">
    </div>
    <pre>{{result}}</pre>
    <button @click="addUser()">Add User</button>
    <button @click="generateRandom()">Generate</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      users: [
        {name: 'Frank'},
        {name: 'John'},
        {name: 'Didier'},
        {name: 'Peter'}
      ],
      finalArray: [],
      result: []
    }
  },
  methods: {
    addUser() {
      this.users.push({name: ''})
    },
    generateRandom() {
      this.finalArray = this.users.map(x => x.name)
      for (let i of this.users) {
        this.randomize(i.name, this.finalArray)
      }
    },
    randomize (user) {
      let index
      do {
        index = Math.floor(Math.random() * this.finalArray.length)
      }
      while (this.finalArray[index] == user) {
        this.result.push({
          santa: user,
          receiver: this.finalArray[index]
        })
        this.finalArray.splice(index, 1)
      }
    }
  }
}
</script>