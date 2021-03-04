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
                Country: {{ data?.All?.country }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Population: {{ parse(data?.All?.population) }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Confirmed Cases: {{ parse(data?.All?.confirmed) }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Deaths: {{ parse(data?.All?.deaths) }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Death Percent: {{ Math.round((data?.All?.deaths / data?.All?.confirmed*100) * 100) / 100 }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Recovered: {{ parse(data?.All?.recovered) }}
              </h1>
            </div>
          </nav>
        </div>
    </div>
    <div class="show">{{ error }}</div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
        country: '',
        data: null,
        show: false,
        error: ''
    }
  },
  methods: {
    submit: function() {
      this.country = this.country.charAt(0).toUpperCase() + this.country.slice(1).toLowerCase();
      console.log(this.country);
      axios(`https://covid-api.mmediagroup.fr/v1/cases?country=${this.country}`)
      .then(res => (this.data = res.data))
      .catch(error => (this.error = error))
      this.show = true;
      
    },
    parse: function(value) {
      return value?.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,')
    }
  }
}
</script>

<style>

.show {
  margin-top: 60px;
}

</style>