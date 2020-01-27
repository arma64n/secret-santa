<template>
  <div class="hello">
    <div v-for="(user, index) in users" :key="index">
      <span>
        {{ index + 1 }}
      </span>
      <input type="text" v-model="user.first">
      <input v-if="user.hasPair" type="text" v-model="user.second">
      <button v-if="!user.hasPair" @click="addPair(user)">Add Pair</button>
      <button v-else @click="removePair(user)">Remove Pair</button>
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
        {first: 'Арма', key: '0', second: "Дами", hasPair: true},
        {first: 'Галым', key: '1', second: "Динка", hasPair: true},
        {first: 'Тима', key: '2', second: "Мэд", hasPair: true},
        {first: 'Нурик', key: '3', second: "Санька", hasPair: true}
      ],
      finalArray: [],
      result: [],
      counter: 0
    }
  },
  methods: {
    addUser() {
      this.users.push({first: ''})
    },
    generateRandom() {
      this.counter++
      if (this.counter > 5) {
        alert('Unsuccessful!')
      }
      let firsts = this.users.map(x => ({name: x.first, key: x.key}))
      let seconds = this.users.map(x => ({name: x.second, key: x.key})).filter(x => x.name)
      let final = [...firsts, ...seconds]
      this.finalArray = [...firsts, ...seconds]
      for (let i of final) {
        this.randomize(i)
      }
    },
    randomize (user) {
      let index
      let counter = 0
      do {
        counter++
        if (this.finalArray.length == 1 && counter > 100) {
          this.result = []
          this.generateRandom()
        }
        index = Math.floor(Math.random() * this.finalArray.length)
      }
      while (this.finalArray[index].name == user.name || this.finalArray[index].key == user.key) {
        this.result.push({
          santa: user.name,
          receiver: this.finalArray[index].name
        })
        this.finalArray.splice(index, 1)
      }
    },
    addPair (pair) {
      this.$set(pair, 'hasPair', true)
    },
    removePair (pair) {
      this.$set(pair, 'hasPair', false)
    }
  }
}
</script>