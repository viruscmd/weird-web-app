<template>
  <section class="section">
    <div class="columns is-desktop is-multiline">

      <div class="column is-full">
        <h1 class="subtitle is-size-6 has-text-grey-light">Running</h1>
        <h2 class="title">Calorie Calculator</h2>
      </div>

      <div class="column">
        <b-field>
          <p class="control">
            <span class="button is-static">Time spent running</span>
          </p>
          <b-timepicker custom-class='has-text-right' expanded enable-seconds hour-format="24" v-model="time">
          </b-timepicker>
        </b-field>

        <b-field>
          <p class="control">
            <span class="button is-static">Distance</span>
          </p>
          <b-input custom-class="has-text-right" type="text" v-model="distance" expanded></b-input>
          <b-select v-model="distanceUnit">
            <option :value="opt.val" v-for="(opt, key) in distanceUnits" :key='key'>
              {{opt.unit}}
            </option>
          </b-select>
        </b-field>

        <b-field>
          <p class="control">
            <span class="button is-static">Weight</span>
          </p>
          <input class='is-expanded has-text-right input' type="number" v-model="weight" expanded></input>
          <b-select v-model="weightUnit">
            <option :value="opt.val" v-for="(opt, key) in weightUnits" :key='key'>
              {{opt.unit}}
            </option>
          </b-select>
        </b-field>
      </div>

      <div class="column is-4-desktop">
        <hr class="is-hidden-desktop">
        <!-- <span class="is-size-2">Calories Burnt:</span>
        <br>
        <span class="is-size-2">{{calories}}</span>  -->

        <p>You burned <strong>{{calories.calories}} calories</strong> on your <strong>{{calories.distance}} {{calories.unit}} run </strong>. At that
          pace, your calorie burn rate is <strong>{{calories.burnRate}} calories </strong> per mile and <strong>{{calories.calsPerHr}}
            calories </strong>per hour.</p>
      </div>

    </div>
  </section>
</template>

<script>
  export default {
    data() {
      return {
        time: new Date('1970-01-01 00:10:00'),
        distance: 1,
        distanceUnits: [{
            unit: 'miles',
            val: 1.60934
          },
          {
            unit: 'km',
            val: 1
          }
        ],
        distanceUnit: 1.60934,
        weight: 300,
        weightUnits: [{
            unit: 'lbs',
            val: 0.453592
          },
          {
            unit: 'kg',
            val: 1
          }
        ],
        weightUnit: 0.453592,
      }
    },
    computed: {
      calories() {
        // Distance
        let distance = parseFloat(this.distance) * this.distanceUnit || 0;
        let unit = this.distanceUnits.filter(x => {
            return x.val == this.distanceUnit
          })[0].unit

        // Duration
        let hrs = (this.time.getHours() * 3600) || 0
        let min = (this.time.getMinutes() * 60) || 0
        let sec = this.time.getSeconds() || 0

        let duration = hrs + min + sec
        console.log(duration);

        // Pace
        let pace = duration / distance
        // Weight
        let weight = parseInt(this.weight) * this.weightUnit

        // Calculations
        let calories = Math.round(distance * weight * 1.036) || 0
        let calsPerKm = Math.round(weight * 1.036) || 0;
        let calsPerMi = Math.round(1.60934 * weight * 1.036) || 0;
        let calsPerHr = Math.round((distance * weight * 1.036) * (3600 / duration)) || 0;
        let burnRate = (unit == 'miles' ? calsPerMi : calsPerKm);

        return {
          calories: calories,
          distance: this.distance,
          unit: unit,
          burnRate: burnRate,
          calsPerHr: calsPerHr,
        }

      }
    }
  }

</script>
