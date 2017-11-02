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

    <!-- map -->
    <gmap-map :center="center" :zoom="16" style="width: 1000px; height: 670px; float: left;">
    <gmap-marker
      :key="index"
      v-for="(m, index) in switchs"
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


      <!-- <gmap-polyline v-for="p in ppath" :key="p.path" :path="p.path" :options="{geodesic:true, strokeColor:'#FF0000'}">
      </gmap-polyline> -->
  </gmap-map>
    <!-- <p v-for="x in ppath" :key="x">{{x.path}}</p> -->
    <!-- <p v-for="x in switchs" :key="x">{{x.name}}</p> -->


    <div style="display: inline-block; margin-left: 20px;">
          <div id="bigBoxs">
              <!-- <div class="row"> -->

               <!-- <div class="col-md-6 col-md-offset-6" > -->
                <h2>Page : <button class="btn btn-default" type="submit">First</button>
                <button class="btn btn-default" type="submit">Previous</button> 1/3 of 5
                <button class="btn btn-default" type="submit">Next</button>
                <button class="btn btn-default" type="submit">Last</button>
                </h2>
              <!-- </div> -->
              <!-- <div class="col-md-6 col-md-offset-6" > -->
              <h2>Status :
                <button class="btn btn-default" type="submit">All</button>
                <button class="btn btn-default" type="submit">Down</button>
                <button class="btn btn-default" type="submit">Up</button>
              </h2>
              <!-- </div> -->
              <!-- <div class="col-md-6 col-md-offset-6" > -->
              <h2>Layer :
                <button class="btn btn-default" type="submit">All</button>
                <button class="btn btn-default" type="submit">Core-End</button>
                <button class="btn btn-default" type="submit">Core-Core</button>
              </h2>
              </div>
              <div class="well well-lg">
              <table class="table table-hover">
                 <thead>
                   <tr>
                     <th>Line_Name</th>
                     <!-- <th>From</th> -->
                     <!-- <th>To</th> -->
                     <th>Status</th>
                   </tr>
                   <!-- <tr>
                     <th>Line_Name</th>
                     <th>From</th>
                     <th>To</th>
                     <th>Distance</th>
                   </tr> -->
                 </thead>
                 <tbody> 
                   <tr v-for="m in switchs":key="m" :clickable="true" >
                    <td :clickable="true">
                      <p v-for="x in switchs" :key="x" :clickable="true">{{x.name}}</p> 
                    </td>
                     <!-- <td>4k_canmparch_sw</td> -->
                     <!-- <td>camp</td> -->
                     <!-- <td>arch</td> -->
                     <td>Up</td>
                   </tr>
                   <!-- <tr>
                     <td>4k_archeng_sw</td>
                     <td>arch</td>
                     <td>eng</td>
                     <td>Up</td>
                   </tr>
                   <tr>
                     <td>4k_engedu_sw</td>
                     <td>eng</td>
                     <td>edu</td>
                     <td>Down</td>
                   </tr> -->
              


                 </tbody>
               </table>
               </div>
              </div>
          </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as VueGoogleMaps from "vue2-google-maps";
import Vue from "vue";

Vue.use(VueGoogleMaps, {
  load: {
    key: "AIzaSyAyCEzPjAsjYJhqnH3Dug9FyWrw6QXXmhs",
    v: "3.26"
    // libraries: 'places', //// If you need to use place input
  }
});

export default {
  data() {
    return {
      center: { lat: 18.79686, lng: 98.9537475 },
      markers: [
        {
          position: { lat: 18.7956453, lng: 98.952812 }
        },
        {
          position: { lat: 18.7982302, lng: 98.9491877 }
        },
        {
          position: { lat: 18.8004538, lng: 98.9504027 }
        },
        {
          position: { lat: 18.7932254, lng: 98.9562057 }
        }
      ],
      plPath: [
        { lat: 18.7956453, lng: 98.952812 },
        { lat: 18.7982302, lng: 98.9491877 },
        { lat: 18.8004538, lng: 98.9504027 },
        { lat: 18.7932254, lng: 98.9562057 },
        { lat: 18.7956453, lng: 98.952812 }
      ],

      ppath: [
        {
          path: [
            { lat: 18.7932254, lng: 98.9562057 },
            { lat: 18.8004538, lng: 98.9504027 }
          ]
        },
        {
          path: [
            { lat: 18.7982302, lng: 98.9491877 },
            { lat: 18.7956453, lng: 98.952812 }
          ]
        },
        {
          path: [
            { lat: 18.8004538, lng: 98.9504027 },
            // { lat: 18.7982302, lng: 98.9491877 }
          ]
        },
        {
          path: [
            { lat: 18.7932254, lng: 98.9562057 },
            { lat: 18.7932254, lng: 98.9562057 }
          ]
        }
      ],

      plvisible: true,
      switchs: [],
      connects: []
    };
  },
  methods: {
    getSwitch() {
      this.axios
        .get("https://fibermap.herokuapp.com/getswitch")
        .then(response => {
          console.log(response.data);
          this.switchs = response.data;
        });
    },
    getConnect() {
      this.axios
        .get("https://fibermap.herokuapp.com/connect")
        .then(response => {
          console.log(response.data);
          this.connects = response.data;
        });
    }
  },
  created: function() {
    this.getSwitch();
    this.getConnect();
  }
};
</script>
