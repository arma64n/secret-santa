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
        let receiver = this.randomize(i.name, this.finalArray)
        this.finalArray = this.finalArray.filter(x => x !== receiver)
      }
    },
    randomize (user) {
      let number = Math.floor(Math.random() * this.finalArray.length)
      if (this.finalArray[number] !== user) {
        this.result.push({
          santa: user,
          receiver: this.finalArray[number]
        })
        return this.finalArray[number]
      } else {
        this.randomize(user)
      }
    }
  }
}
</script>