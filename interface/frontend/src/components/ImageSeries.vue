<template>
<div class="container">
  <div class="row">
    <div class="col-md-12">
      <div class="card">
        <div class="card-block">
          <h3 class="card-title">Available image series</h3>
          <template v-if="availableSeries.length">
            <ul>
              <li v-for="series in availableSeries">
                <a href="#" @click="selectSeries(series)">{{ series.series_instance_uid }}</a>
                <span v-if="series == selected">&larr;</span>
              </li>
            </ul>
          </div>
        </div>
      </div><!-- left side -->
      <div class="col-md-8">
        <div class="row">
          <div class="col-md-12">
            <div class="card">
              <div class="card-block">
                <h3 class="card-title">Available image series</h3>
                <template v-if="availableSeries.length">
                  <ul>
                    <li v-for="series in availableSeries">
                      <a href="#" @click="selectSeries(series)">{{ series.series_instance_uid }}</a>
                      <span v-if="series == selected">&larr;</span>
                    </li>
                  </ul>
                </template>
                <template v-else>
                  <p class="card-text">No images available.</p>
                </template>
              </div>
            </div>
          </div>
        </div>
        <div class="row" v-if="selected">
          <div class="col-md-12">
            <div class="card">
              <div class="card-block">
                <h3 class="card-title">{{ selected.patient_id }}</h3>
                <p class="card-text">

                <table class="table table-bordered">
                  <thead></thead>
                  <tr>
                    <th>key</th>
                    <th>value</th>
                  </tr>
                  <tbody>
                  <tr v-for="(item, key, index) in selected">
                    <td>{{ key }}</td>
                    <td>{{ item }}</td>
                  </tr>
                  </tbody>
                </table>

                </p>
                <a href="#" class="btn btn-primary">Start case</a>
              </div>
            </div>
          </div>
        </div>
      </div><!-- right side -->
    </div>
  </div>
</div>
</template>

<script>
export default {
  data () {
    return {
      availableSeries: [],
      directoriesDict: {},
      selected: null
    }
  },
  created () {
    this.fetchData()
    this.fetchAvailableImages()
  },
  methods: {
    fetchData () {
      this.$http.get('/api/images/').then(
        (response) => {
          this.availableSeries = response.body
        },
        () => {
          // error callback
        })
    },
    selectSeries (series) {
      console.log(series.uri)
      this.selected = series
    },
    fetchAvailableImages () {
      this.$http.get('/images/available').then(
        (response) => {
          this.directoriesDict = response.body
        },
        () => {
          // error callback
        }
      )
    }
  }
}
</script>

<style>
</style>
