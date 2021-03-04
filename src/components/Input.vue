<template>
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
        <div v-if="show">
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
                Population: {{ data.data.All.population }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Confirmed Cases: {{ data.data.All.confirmed }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Recovered: {{ data.data.All.recovered }}
              </h1>
            </div>
            <div class="panel-block">
              <h1 class="control">
                Deaths: {{ data.data.All.deaths }}
              </h1>
            </div>
          </nav>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    methods: {
        submit: function() {
            axios("https://covid-api.mmediagroup.fr/v1/cases?country=Italy")
            .then(res => this.data = res)
            this.show = true;
        }
    },
    data() {
        return {
            country: '',
            data: {},
            show: false
        }
    }
}
</script>