
<template>
    <Page>
        <ActionBar title="nearBuy"/>
        <GridLayout columns="*" rows="*">
            <Label class="message" :text="msg" col="0" row="0"/>
            <Button text="Next" @tap="onButtonTap" />
        </GridLayout>
    </Page>
</template>

<script>
    //Importing the map component
    import Map from './map'
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
