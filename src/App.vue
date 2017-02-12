<template>
    <div id="app">
        <input-bar
          v-on:subredditEntered="subredditEntered"
        ></input-bar>
        <subreddit-list
            :subreddits="subreddits"
            @removeSubreddit="removeSubreddit"
        ></subreddit-list>
        <image-list
            :posts="posts"
            :subreddits="subreddits"
        ></image-list>
    </div>
</template>

<script>
import InputBar from './components/InputBar'
import SubredditList from './components/SubredditList'
import ImageList from './components/ImageList'

import _ from 'lodash'
import axios from 'axios'

export default {
    name: 'app',
    components: {
        'input-bar': InputBar,
        'subreddit-list': SubredditList,
        'image-list': ImageList
    },
    data: function() {
        return {
            subreddits: [],
            posts: []
        }
    },
    methods: {
        subredditEntered: function(subreddit) {
            this.subreddits.push(subreddit);
            this.posts = [];
            this.getImages();
        },
        removeSubreddit: function(subreddit) {
            this.subreddits.splice(this.subreddits.indexOf(subreddit), 1);
            this.posts = [];
            this.getImages();
        },
        getImages: _.debounce(function() {
            if (!this.subreddits.length) {
                return;
            }
            var subreddits = this.subreddits.join('+'),
                self = this;
            axios.get('http://api.reddit.com/r/' + subreddits + '/hot')
                .then(function(response) {
                    response = response.data;
                    if (response.data && response.data.children) {
                        self.posts = response.data.children;
                    }
                })
                .catch(function(error) {
                    console.error(error);
                });
        }, 500)
    }
}
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}
img {
    height: 100px;
}
</style>
