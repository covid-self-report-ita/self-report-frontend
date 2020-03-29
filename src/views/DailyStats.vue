<template>
  <div v-if="data">
    <h3>Daily stats</h3>

    <!-- Add your visualization code here -->

    <table>
      <thead>
      <tr>
        <th>Day</th>
        <th>healthy</th>
        <th>sick_guess_no_corona</th>
        <th>sick_guess_corona</th>
        <th>sick_corona_confirmed</th>
        <th>recovered_not_confirmed</th>
        <th>recovered_confirmed</th>
      </tr>
      </thead>

      <tbody>
      <tr v-for="(dayData, day) in dailyStats">
        <td>
          {{ day }}
        </td>
        <td>
          {{ dayData.total_healthy }}
        </td>
        <td>
          {{ dayData.total_sick_guess_no_corona }}
        </td>
        <td>
          {{ dayData.total_sick_guess_corona }}
        </td>
        <td>
          {{ dayData.total_sick_corona_confirmed }}
        </td>
        <td>
          {{ dayData.total_recovered_not_confirmed }}
        </td>
        <td>
          {{ dayData.total_recovered_confirmed }}
        </td>
      </tr>
      </tbody>
    </table>

  </div>
</template>

<script>

  export default {
    name: "daily-stats",
    components: {},
    props: {
      data: Array,
    },
    mounted: function () {
    },
    computed: {
      dailyStats() {

        const dailyStats = {};
        for (const locationData of this.data) {

          if (locationData.date === '') {
            continue;
          }

          if (dailyStats[locationData.date] === undefined) {
            dailyStats[locationData.date] = {
              total_healthy: 0,
              total_sick_guess_no_corona: 0,
              total_sick_guess_corona: 0,
              total_sick_corona_confirmed: 0,
              total_recovered_not_confirmed: 0,
              total_recovered_confirmed: 0,
            }
          }

          dailyStats[locationData.date].total_healthy += locationData.total_healthy;
          dailyStats[locationData.date].total_sick_guess_no_corona += locationData.total_sick_guess_no_corona;
          dailyStats[locationData.date].total_sick_guess_corona += locationData.total_sick_guess_corona;
          dailyStats[locationData.date].total_sick_corona_confirmed += locationData.total_sick_corona_confirmed;
          dailyStats[locationData.date].total_recovered_not_confirmed += locationData.total_recovered_not_confirmed;
          dailyStats[locationData.date].total_recovered_confirmed += locationData.total_recovered_confirmed;
        }

        return dailyStats;
      }

    },
  }
</script>

<style scoped>

  td, th {
    border: white solid 1px;
    padding: 5px;
  }
</style>

