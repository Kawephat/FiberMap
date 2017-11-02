<template>
  <div id="app">
    <nav class="navbar navbar-inverse navbar-fixed-top">
        <div class="container-fluid">
      <div class="navbar-header">
        <a class="navbar-brand" href="#"><h4>Fiber Map</h4></a>
      </div>
      <ul class="nav navbar-nav">
        <li class="active"><a href="#"><h4>Monitor</h4></a></li>
        <li><a href="#"><h4>Real Path</h4></a></li>
      </ul>
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#"><h4><span class="glyphicon glyphicon-log-in"></span> Login</h4></a></li>
      </ul>
    </div>
    </nav>
    <br><br><br><br>
    <gmap-map
    :center="center"
    :zoom="16"
    style="width: 800px; height: 670px"
  >
    <gmap-marker
      :key="index"
      v-for="(m, index) in markers"
      :position="m.position"
      :clickable="true"
      :draggable="true"
      @click="center=m.position"
    ></gmap-marker>


    <!-- <gmap-polyline
      :key="index"
      v-for="(p, index) in polyline"
      :position="p.position"
      :path="p.path"
      :clickable="true"

    ></gmap-polyline> -->
     <gmap-polyline  v-if="plvisible" :path="plPath" :options="{geodesic:true, strokeColor:'#FF0000'}">
    </gmap-polyline>
  </gmap-map>

    <p v-for="x in sources" :key="x.name">{{x.name}}</p>
  </div>
</template>

<script>
    import * as VueGoogleMaps from 'vue2-google-maps';
    import Vue from 'vue';

  Vue.use(VueGoogleMaps, {
    load: {
      key: 'AIzaSyAyCEzPjAsjYJhqnH3Dug9FyWrw6QXXmhs',
      v: '3.26',
      // libraries: 'places', //// If you need to use place input
    }
  });
 
  export default {
    data () {
      return {
        center: {lat: 18.79686, lng: 98.9537475},
        markers: [{
            position: {lat: 18.7956453, lng: 98.952812}
          }, {
            position: {lat: 18.7982302, lng: 98.9491877}
          }, {
            position: {lat: 18.8004538, lng: 98.9504027}
          }, {
            position: {lat: 18.7932254, lng: 98.9562057}
          }],
        plPath: [
        {lat: 18.7956453, lng: 98.952812},
        {lat: 18.7982302, lng: 98.9491877},
        {lat: 18.8004538, lng: 98.9504027},
        {lat: 18.7932254, lng: 98.9562057}
      ],
      plvisible: true,
      sources: [],
      
      
      }

    },
    created: function () {
    this.axios.get('http://samples.openweathermap.org/data/2.5/weather?q=London,uk&appid=b1b15e88fa797225412429c1c50c122a1').then((response) => {
  console.log(response.data)
})
  }
  }
</script>
