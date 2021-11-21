<template>
  <div class="page-clients">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="title">Clients</h1>

        <router-link class="button is-light mt-4" :to="{ name: 'AddClient'}">Add client</router-link>
      </div>

      <div class="column is-3" v-for="client in clients" v-bind:key="client.id">
        <div class="box">
          <h3 class="is-size-4 mb-4">{{ client.name }}</h3>

          <router-link class="button is-light" :to="{ name: 'Client', params: { id: client.id }}">Details</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Clients',
  data() {
    return {
      clients: []
    }
  },
  mounted() {
    this.getClients()
  },
  methods: {
    getClients() {
      axios
        .get('/api/v1/clients/')
        .then(response => {
          for (let i = 0; i < response.data.length; i++) {
            this.clients.push(response.data[i])
          }
        })
        .catch(error => {
          console.log(JSON.stringify(error))
        })
    }
  }
}
</script>

<style scoped>

</style>