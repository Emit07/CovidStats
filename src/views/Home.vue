<template>
  <div>
    <div>
        <nav class="panel form">
            <p class="panel-heading">
                Search
            </p>
            <form @submit.prevent="submit">
                <div class="panel-block">
                    <p class="control">
                        <input v-model="country" class="input" type="text" placeholder="country" required>
                    </p>
                </div>
                <div class="panel-block">
                    <button class="button is-fullwidth is-light">
                    Search
                    </button>
                </div>
            </form>
        </nav>
        <div v-if="show" class="show">
          <nav class="panel form post">
            <p class="panel-heading">
              Covid-19 Stats
            </p>
            <div class="panel-block">
              <h1 class="control">
                Country: {{ data.data.All.country }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Population: {{ parse(data.data.All.population) }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Confirmed Cases: {{ parse(data.data.All.confirmed) }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Deaths: {{ parse(data.data.All.deaths) }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Death Percent: {{ Math.round((data.data.All.deaths / data.data.All.confirmed*100) * 100) / 100 }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Recovered: {{ parse(data.data.All.recovered) }}
              </h1>
            </div>
          </nav>
        </div>
    </div>
    {{ error }}
  </div>
</template>

<script>
import axios from 'axios';

export default {
  methods: {
    submit: function() {
      axios(`https://covid-api.mmediagroup.fr/v1/cases?country=${this.country}`)
      .then(res => (this.data = res))
      .catch(error => this.error = error)
      this.show = true;
    },
    parse: function(value) {
      return value.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,')
    }
  },
  data() {
      return {
          country: '',
          data: {},
          show: false,
          error: ''
      }
    }
}
</script>

<style>

.show {
  margin-top: 60px;
}

</style>