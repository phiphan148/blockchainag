<template>
  <div class="home">
    <v-container fluid grid-list-lg>
      <Banner></Banner>
      <div v-for="(tweet, index) in mainData" :key="index">
        <TweetDetails v-bind:tweet="tweet"></TweetDetails>
      </div>
    </v-container>
  </div>
</template>

<script>
    import TweetDetails from "../components/TweetDetails";
    import Banner from "../components/Banner";
    export default {
        name: "Home",
        components: {TweetDetails, Banner},
        data() {
            return {

            }
        },
        computed: {
            mainData() {
                return this.$store.state.mainData;
            },
            infoData() {
                return this.$store.state.info;
            }
        },
        methods: {
            toTweet(id) {
                this.$store.commit('tweetId', id);
                console.log(this.$store.state.id);
                this.$router.push('/tweet');
            }
        }
    };
</script>

<style>
  p {
    margin: 0px;
  }
</style>