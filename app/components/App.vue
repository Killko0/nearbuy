
<template>
    <Page>
        <ActionBar title="nearBuy"/>
        <WrapLayout>
            <TextField :text="msg" hint="Enter a product..." />
            <Button text="Search" @tap="onButtonTap" />
            <ListView for="item in items" @itemTap="onItemTap">
            <v-template>
            <!-- Shows the list item label in the default color and style. -->
            <Label :text="item.message" />
            </v-template>
            </ListView>
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
   
    let rawInput = "post it";
    //Splitting raw input into words
    let splitInput = rawInput.split(" ");
    let searchProductResults = [];
    for (let word of splitInput) {
        console.log(word);
                //ASYNC
                productsCollection.where("tags", "array-contains", word).get().then(function(querySnapshot) {
                    querySnapshot.forEach(function(doc) {
                        searchProductResults.push("hello");
                        console.log('1');
                        // doc.data() is never undefined for query doc snapshots

                        console.log(searchProductResults);
                        searchProductResults.forEach(function(product){
                            //if (product.data().barcode !== doc.data().barcode) {
                               
                           // }
                        })
                        
                       
                    });
                })


                .catch(function(error) {
                    console.log("Error getting documents: ", error);
                });        
    }

    
     /* productsCollection.get().then(querySnapshot => {
        querySnapshot.forEach(doc => {
          console.log(`${doc.id} => ${JSON.stringify(doc.data())}`);
        });
      });*/
      
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
        msg: 'Enter article..',
        items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
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
