<template>
    <Page class="page">
        <ActionBar class="action-bar" title="nearBuy"></ActionBar>
        <GridLayout>
                <Mapbox
                    accessToken="pk.eyJ1IjoiZW1pbHNhbGxlbSIsImEiOiJjam5rZ3BibnMwZjZmM3dwazhsM29pcWg2In0.Kn7kBXDI7niAIHvwS2iDMw"
                    mapStyle="traffic_day"
                    latitude="37.7397"
                    longitude="-121.4252"
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
    import * as utils from "utils/utils";
    export default {
        props: {
            name: {
                type: String
            },
            textFieldValue: ""
        
        },
        data () {
            return { };
        },
        methods: {
            onMapReady(args) {
                console.log(this.name);
                args.map.addMarkers([
                    {
                        lat: 37.7397,
                        lng: -121.4252,
                        title: "Tracy, CA",
                        subtitle: "Home of The Polyglot Developer!",
                        onCalloutTap: () => {
                            utils.openUrl("https://www.thepolyglotdeveloper.com");
                        }
                    }
                ]);
            }
        }
    };

</script> 
 

