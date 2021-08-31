<template>
  <div class="table__wrapper">
    <table class="table">
      <thead>
        <tr>
          <th></th>
          <th>Title</th>
          <th>Release Date</th>
          <th>Box Office</th>
          <th>Duration</th>
          <!--<th>Overview</th> -->
          <th>Trailer Link</th>
          <th>Director</th>
          <th>Phase</th>
          <th>Saga</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <template v-for="(item, index) in mcu" :key="index" >
          <tr :class="[{'new': '2021-05-05' < item.release_date}, {'huge': parseInt(item.box_office) > 1000000000 }]"  v-if="item.title != 'Guardians of the Galaxy Vol. 3'">
            <td><img v-if="item.cover_url" :src="item.cover_url"/></td>
            <td>{{item.title}}</td>
            <td>{{item.release_date}}</td>
            <td>{{numberWithCommas(item.box_office)}}</td>
            <td>{{item.duration}} minutes</td>
            <!--<td>{{item.overview}}</td>-->
            <td><a v-if="item.trailer_url" :href="item.trailer_url" target="_blank">Trailer</a></td>
            <td>{{item.directed_by}}</td>
            <td>{{item.phase}}</td>
            <td>{{item.saga}}</td>
            <td><a v-if="item.imdb_id" :href="'https://www.imdb.com/title/' + item.imdb_id" target="_blank">IMDB</a></td>
            </tr>
        </template>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data: () => ({
    mcu: {}
	}),  
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    numberWithCommas(x) {
      return '$' + x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
  },
  created() {

     axios({
        method: 'get',
        url: 'https://mcuapi.herokuapp.com/api/v1/movies?order=chronology%2CDESC'
      }
      ).then(response => {

        this.mcu = response.data.data;

      }).catch(error => {
          if (error.response ) {
          }
      }); 
      

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
 
</style>
