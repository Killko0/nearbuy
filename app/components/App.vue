
<template>
    <Page>
        <ActionBar title="nearBuy"/>
        <WrapLayout>
            <TextField :text="textFieldValue" hint="Enter a product..." />
            <Button text="Search" @tap="onButtonTap" />
        </WrapLayout>
    </Page>
</template>


<script>
    
    //Importing the map component
    import Map from './map'
    
    //Wiring firebase
    const firebase = require("nativescript-plugin-firebase");
 
    firebase.init({
     // Optionally pass in properties for database, authentication and cloud messaging,
     // see their respective docs.
    }).then(
    function (instance) {
      
      

      console.log("firebase.init done");
      //Looping over collection and display/get all data in it
      var productsCollection = firebase.firestore.collection("products");
      productsCollection.get().then(querySnapshot => {
        querySnapshot.forEach(doc => {
          console.log(`${doc.id} => ${JSON.stringify(doc.data())}`);
        });
      });
      
    },
    function (error) {
      console.log("firebase.init error: " + error);
    }
);
    export default {
        methods: {
            onButtonTap() {
            this.$navigateTo(Map);
        }
    },
    data() {
      return {
        msg: 'Hello World!'
      }
    }
  }



</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
</style>
