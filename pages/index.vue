<template>
  <div>
    <Tutorial/>
    <button @click="getFirebase">Access Firebase</button>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  methods: {
    async getFirebase() {
      const query = await this.$fire.firestore.collection('data').get()
      try {
        const docs = []
        query.forEach((doc) => {
          var data = doc.data()
          var record = [doc.id, data.id, data.name]
          console.log(record)
          docs.push(record)
        })
        this.message = docs
      } catch (err) {
        console.log('failed to fetch data from firebase.')
      }
    }
  },
}
</script>
