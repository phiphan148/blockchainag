<template>
    <div class="tweet-component">
        <div fluid grid-list-lg>
            <div class="tweet-content shadow-sm bg-white">
                <div class="row">
                    <div class="col-4 col-sm-2 not-show-mb title-color">
                        <p>{{tweet.created_at}}</p>
                    </div>
                    <div class="col">
                        <p class="test pb-2" style="margin: 0px">{{tweet.text}}</p>
                        <div class="tweet-img" v-if="tweet.link_text && tweet.photo_link_text">
                            <v-hover>
                                <div slot-scope="{ hover }" :class="`elevation-${hover ? 12 : 2}`" class="mx-auto">
                                    <a href=tweet.link_text><img width="100%" :src=tweet.photo_link_text alt="link img"></a>
                                    <div class="tweet-img-title">
                                        <p href=tweet.link_text>{{tweet.link_text}}</p>
                                    </div>
                                </div>
                            </v-hover>
                        </div>
                        <p class="pr-1 title-color hashtag" v-for="hash in tweet.entities.hashtags">#{{hash}}</p>
                        <div style="clear: both"></div>
                        <p class="not-show title-color" style="margin: 0px">{{tweet.created_at}}</p>
                        <div class="row">
                            <div class="popUp col-5" v-for="img in tweet.media_image">
                                <img @click="modalPop(img)" class="img-fuild " :src=img.src alt="img">
                            </div>
                            <modal v-if="showModal" @close="showModal = false">
                                <div slot="header">
                                    <img class="card-image img-fluid" style="position: relative" :src="modalDetail" alt="cover">
                                </div>
                            </modal>
                        </div>

                        <div class="row social pt-1" @click="toTweet(tweet.id)">
                            <div class="col"><i class="far fa-comments"></i><span class="static"> Comment</span></div>
                            <div class="col"><i class="fas fa-retweet"></i> {{tweet.retweet_count}}</div>
                            <div class="col"><i class="far fa-heart"></i> {{tweet.favorite_count}}</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import modal from './modal.vue';

    export default {
        name: "TweetDetails",
        components: {modal},
        data() {
            return {
                showModal: false,
            }
        },
        props: {
            data: Array,
            tweet: Object,
        },
        computed: {},
        methods: {
            toTweet(id) {
                this.$store.commit('tweetId', id);
                console.log(this.$store.state.id);
                console.log(typeof this.$store.state.id);
                this.$router.push('/tweet');
            },
            modalPop(item) {
                this.showModal = true;
                this.modalDetail = item.src;
            },
        }
    };
</script>

<style>
    @media only screen and (max-width: 575px) {
        .social {
            text-align: center;
        }
    }

    @media only screen and (min-width: 576px) {
        .not-show {
            display: none;
        }

        .social {
            cursor: pointer;
        }
    }

    p {
        margin: 0px;
    }

    .popUp img {
        width: 100%;
    }
</style>
