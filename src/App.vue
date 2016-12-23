<template>
  <div id="preappCalc" class="container">
    <!-- if preappChoices v-model is false, then show it -->
    <div id="preappDetails" v-if="!preappChoices">
      <h1>Your Details</h1>
      <hr>
      <h2>Set your retirement timeframe</h2>
      <div class="form-group">
        <label>Current age</label>
        <input type="number" 
                class="form-control" 
                v-model="age">
      </div>
      <div class="form-group">
        <label>Planned retirement age</label>
        <input type="number" 
                class="form-control" 
                v-model="retirementAge">
      </div>
      <h2>Set Your Contributions</h2>
      <div class="form-group">
        <label>Current value of existing pensions</label>
        <input type="number" 
                class="form-control" 
                v-model="currentPensionsValue">
      </div>
      <fieldset class="form-group">
        <legend>Are you or your employer paying into your pensions?</legend>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" 
                    class="form-check-input" 
                    name="employerContrib" 
                    id="employerContrib"
                    v-model="employerContrib"
                    :value="true"> 
            Yes
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" 
                    class="form-check-input" 
                    name="employerContrib" 
                    id="employerContrib"
                    v-model="employerContrib"
                    :value="false">
            No
          </label>
        </div>
      </fieldset>

      <!-- if employerContrib is truthy - display the amount field -->
      <div class="form-group" v-if="employerContrib">
        <label>Approximate total amount being paid in</label>
        <input type="number" 
                name="employerAmount" 
                v-model="employerAmount" 
                class="form-control">
      </div>
      <!-- // end conditional block display -->

      <div class="form-group">
        <label>One-off contribution</label>
        <input class="form-control" 
                type="number" 
                name="oneOffContrib" 
                v-model="oneOffContrib">
      </div>
      <fieldset class="form-group">
        <legend>The state pension</legend>
        <p class="lead">We can include......</p>
        <label>Would you like to include the state pension?</label>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" 
                    class="form-check-input" 
                    name="statePension" 
                    id="statePension" 
                    v-model="statePension" 
                    :value="true">
            Yes
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input type="radio" 
                    class="form-check-input" 
                    name="statePension" 
                    id="statePension" 
                    v-model="statePension" 
                    :value="false">
            No
          </label>
        </div>
      </fieldset>
      <p class="text-xs-right">
        <button type="button" class="btn  btn-primary" 
                @click="preappChoices = !preappChoices">Calculate</button>
      </p>
    </div>
    <!-- // .preappDetails -->

    <div id="preappChoices" v-if="preappChoices">

      <div class="alert alert-info" role="alert">
        <strong>£ {{ potValue }}</strong>
         <button type="button" class="btn  btn-primary" 
                @click="preappChoices = !preappChoices">Edit details</button>
      </div>

      <div class="form-group">
        <label class="col-xs-12">Expected growth rate</label> 
        <ul class="list-inline">
          <li class="list-inline-item" v-for="percent in percentages">
            <button type="button" class="btn">{{ percent.percent }}%</button>
          </li>
        </ul> 
      </div>

      <Chart  :labels="[39, 45 , 55, 60, 65, 70]" 
              :values="[5, 10, 20, 30, 40, 50, 60]" 
              :chartType="['area']"
              :chartTitle="['']">
              </Chart>
    
      <button type="button" class="btn btn-primary" @click="togglePreappInfo">{{ editPreappInfo ? hidePreappInfoText : editPreappInfoText }}</button>

      <div class="card" v-if="editPreappInfo">
        <ul class="list-group  list-group-flush">
          <li class="list-group-item form-group">
            <label>Planned retirement age</label>
            <input class="form-control" type="number" name="retirementAge" v-model="retirementAge">
          </li>
          <li class="list-group-item form-group">
            <label>One-off contribution</label>
            <input class="form-control" type="number" name="oneOffContrib" v-model="oneOffContrib">
          </li>
          <li class="list-group-item form-group">
            <label>Regular contribution</label>
            <input class="form-control" type="number" name="regularContrib" v-model="regularContrib">
          </li>
        </ul>
      </div>

    </div>
    <!-- // .preappChoices -->

  </div>
  <!-- // #preappCalc -->

</template>

<script>

import Chart from './components/Chart.vue'

export default {
  name: 'app',
  components: { Chart },
  data () {
    return {
      age: '',
      retirementAge: 55,
      currentPensionsValue: '',
      payingInto: false,
      oneOffContrib: '',
      statePension: null,
      preappChoices: false,
      editPreappInfo: false,
      editPreappInfoText: 'Edit info',
      hidePreappInfoText: 'Hide info',
      employerAmount: '',
      employerContrib: null,
      percentages: [
        { percent: 3 },
        { percent: 5 },
        { percent: 8 }
      ],
    }
  },
  computed: {
    potValue: function() {
      return this.currentPensionsValue * this.oneOffContrib;
    }
  },
  methods: {
    togglePreappInfo: function() {
      this.editPreappInfo = !this.editPreappInfo
    }
  }
}
</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
