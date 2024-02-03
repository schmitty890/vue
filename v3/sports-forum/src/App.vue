<script>
export default {
  {
      data: () => ({
        newSport: {
          name: '',
          insideOrOutside: []
        },
        sportsList: [{
          name: 'hockey',
          insideOrOutside: ['Indoors']
        },{
          name: 'skateboarding',
          insideOrOutside: ['Outdoors']
        },{
          name: 'baseball',
          insideOrOutside: ['Outdoors']
        },{
          name: 'football',
          insideOrOutside: ['Outdoors']
        },{
          name: 'basketball',
          insideOrOutside: ['Indoors']
        }],
        favoriteList: []
      }),
      computed: {
        benderStatistics() {
          const location = ['Indoors', 'Outdoors'];
          const statistics = {
            Indoors: 0,
            Outdoors: 0,
          }
          this.sportsList.forEach( sport => {
            location.forEach(insideOrOutside => {
              if(sport.insideOrOutside.indexOf(insideOrOutside) > -1) {
                statistics[insideOrOutside] += 1;
              }
            });
          })
          return statistics;
        }
      },
      methods: {
        favoriteSport(sport) {
          console.log('fav sport')
          this.favoriteList.push(sport)
        },
        addNewSport() {
          console.log('add new sport')
          this.sportsList.push(this.newSport)
          this.newSport = { name: '' }
        },
      }
    }
}
</script>

<template>
  <div>
    <h2>Statistics</h2>
    <ul>
      <li>Indoors: {{ benderStatistics.Indoors }}</li>
      <li>Outdoors: {{ benderStatistics.Outdoors }}</li>
    </ul>

    <ul>
      <li v-for="(stat, type) in benderStatistics">{{ type }}: {{ stat }}</li>
    </ul>
    {{ benderStatistics }}
    <h2>Sports!</h2>
    <p v-if="sportsList.length === 0">There are no sports to list . . .</p>
    <ul v-else>
      <li v-for="sport in sportsList">
        <p>{{ sport.name }}</p>
        <button @click="favoriteSport(sport)">⭐ Favorite</button>
      </li>
    </ul>
    <h2>Favorite sports</h2>
    <ul v-if="favoriteList.length > 0">
      <li v-for="sport in favoriteList">
        <p>{{ sport.name }}</p>
      </li>
    </ul>
    <p v-else>No favorite sports list yet . . .</p>
    <h2>New sport</h2>
    <label for="sport-name">Name</label>
    <pre>
      {{ newSport }}
    </pre>
    <input type="text" v-model="newSport.name" @keyup.enter="addNewSport" />
  </div>
</template>
