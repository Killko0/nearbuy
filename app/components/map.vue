<template>
    <Page class="page">
        <ActionBar class="action-bar" title="nearBuy"></ActionBar>
        <GridLayout>
                <Mapbox
                    accessToken="pk.eyJ1IjoiZW1pbHNhbGxlbSIsImEiOiJjam5rZ3BibnMwZjZmM3dwazhsM29pcWg2In0.Kn7kBXDI7niAIHvwS2iDMw"
                    mapStyle="traffic_day"
                    latitude="52.493997"
                    longitude="13.446464"
                    hideCompass="true"
                    zoomLevel="12"
                    showUserLocation="false"
                    disableZoom="false"
                    disableRotation="false"
                    disableScroll="false"
                    disableTilt="false"
                    @mapReady="onMapReady($event)">
                </Mapbox>
        </GridLayout>
    </Page>
</template>


<script>
const firebase = require("nativescript-plugin-firebase");

console.log("im map");
import * as utils from "utils/utils";
export default {
  props: {
    barcode: {
      type: String
    },
    textFieldValue: ""
  },
  data() {
    return {};
  },
  methods: {
    onMapReady(args) {
      console.log(this.barcode);

      var storesCollection = firebase.firestore.collection("stores");
      storesCollection
        .where("products", "array-contains", this.barcode)
        .get()
        .then(function(querySnapshot) {
          querySnapshot.forEach(function(doc) {
            console.log(doc.data());
            args.map.addMarkers([
              {
                lat: doc.data().xcord,
                lng: doc.data().ycord,
                title: doc.data().name,
                subtitle: "Home of The Polyglot Developer!",
                onCalloutTap: () => {
                  utils.openUrl("https://www.thepolyglotdeveloper.com");
                }
              }
            ]);
          });
        });
    }
  }
};
</script> 
 

