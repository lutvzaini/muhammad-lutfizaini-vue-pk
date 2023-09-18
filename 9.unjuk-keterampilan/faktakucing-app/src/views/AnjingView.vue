<template>
<div id="app">
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1>Dog Facts</h1>
        <ul class="list-group">
          <li class="list-group-item" v-for="fact in facts" :key="fact.id">
            {{ fact.fact }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</div>
</template>

<script>
const app = new Vue({
  el: '#app',
  data: {
    facts: []
  },
  mounted() {
    this.fetchFacts();
  },
  methods: {
    async fetchFacts() {
      const response = await axios.get('https://dogapi.dog/api/v2/facts?limit=3');
      this.facts = response.data.facts;
    }
  }
});
</script>
