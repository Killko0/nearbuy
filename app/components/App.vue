
<template>
    <Page>
        <ActionBar title="nearBuy"/>
        <WrapLayout>
            <TextField v-model="textFieldValue" hint="Enter a product..." />
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
    

    function search(rawInput){

        //Looping over collection and display/get all data in it
        var productsCollection = firebase.firestore.collection("products");
   
        //Splitting raw input into words
        let splitInput = rawInput.split(" ");
        let searchProductResults = [];
   
        //Looping over every searched word
        for (let word of splitInput) {
            console.log(word);
                
            //Looping over each found element
            productsCollection.where("tags", "array-contains", word).get().then(function(querySnapshot) {
                querySnapshot.forEach(function(doc) {
                       
                // doc.data() is never undefined for query doc snapshots
                if (searchProductResults.length == 0) {
                    searchProductResults.push(doc.data());
                }
                else {
                    let found = false;
                    searchProductResults.forEach(function(product){
                                
                        if (product.barcode == doc.data().barcode) {
                                   found = true; 
                                }
                            })
                            if(found) {
                                searchProductResults.push(doc.data());
                            }
      
 
                            
                        }
                       
                        
                       
                    });
                    console.log(searchProductResults)
                })

                
                .catch(function(error) {
                    console.log("Error getting documents: ", error);
                }); 
    }
    };

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
        search();


      
    },
    function (error) {
      console.log("firebase.init error: " + error);
    }
);
    export default {
        methods: {
            onButtonTap() {
                console.log(this.$data.textFieldValue);
                search(this.$data.textFieldValue);
                //this.$navigateTo(Map);
            }
        },
        data() {
            return {
                textFieldValue: "",
                items: [
                    { message: 'Foo' },
                    { message: 'Bar' }
                ]

            }
        },

        created() {
            console.log("created!");
            
            

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
