<template>
  <v-container>
    <v-row class="text-center" v-if="!loading && launch != null">
      <v-col class="mb-4 mt-4">
        <h1 class="display-2 mb-3">Latest SpaceX launch</h1>
        <v-card class="mx-auto mt-8" max-width="1000" >
          <v-img
            class="white--text align-end"
            height="300px"
            src="../assets/launch.png"
          >
            <v-card-title>{{ launch.name }}</v-card-title>
          </v-img>
          <v-card-subtitle class="pb-0 text-left">Date: {{ dateLaunch }}</v-card-subtitle>

          <v-card-text class="text--primary align-start text-left mt-2 text-justify">
            <div>{{ this.launch.details }}</div>
          </v-card-text>
          <div v-if="ships != null">
            <h4 class="mt-3 pb-3">Info about ships</h4>
            <v-data-table
              :headers="headers"
              :items="ships"
              :items-per-page="5"
              class="elevation-1"
            />
          </div>
          <div v-else>
            <h4 class="mt-10 pb-10">No ships available</h4>
          </div>
        </v-card>
      </v-col>
    </v-row>
    <div class="text-center" v-else>
      <div class="mt-10"/>
      <v-progress-circular
      :size="200"
      :width="7"
      color="black"
      indeterminate />
    </div>
  </v-container>
</template>

<script>
export default {
  name: 'Info',
  created() {
    this.axios.get('/launches/latest')
      .then((response) => {
        this.launch = response.data;
        const ships = response.data.ships;
        if(ships.length > 0) {
          let shipsInfo = [];
          ships.forEach(async ship => {
            try {
              const responseShip = await this.axios.get(`/ships/${ship}`);
              shipsInfo.push(responseShip.data);
            } catch (error) { alert('Error fetching ship: ' + ship); }
          });
          this.ships = shipsInfo;
          this.loading = false;
        }
      })
      .catch((error) => alert('Error fetching latest launch') )
  },
  computed: {
    dateLaunch: function () {
      const date = new Date(this.launch.date_unix * 1000);
      let hours = date.getHours();
      let minutes = date.getMinutes();
      if (hours < 10) hours = '0'+hours;
      if (minutes < 10) minutes = '0'+minutes;
      let day = date.getDay();
      let month = date.getMonth() + 1;
      if (day < 10) day = '0'+day;
      if (month < 10) month = '0'+month;
      const year = date.getFullYear();
      return `${day}/${month}/${year} - ${hours}:${minutes}`;
    }
  },
  data: () => ({
    launch: null,
    loading: true,
    ships: null,
    headers: [
      { text: 'Name', value: 'name' },
      { text: 'Type', value: 'type' },
      { text: 'Home Port', value: 'home_port' }
    ],
  }),
}
</script>
