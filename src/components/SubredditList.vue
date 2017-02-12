<template>
    <div class="subreddit-list">
        <li v-for="name in subreddits">
            {{name}}
            <span v-on:click="removeSubreddit(name)">x</span>
        </li>
        <span class="empty" v-if="!this.subreddits.length">
            enter a subreddit to get started!
        </span>
    </div>
</template>

<script>
    export default {
        name: 'subreddit-list',
        props: ['subreddits'],
        methods: {
            removeSubreddit: function(name) {
                this.$emit('removeSubreddit', name);
            }
        }
    }
</script>

<style scoped>
.subreddit-list {
    display: flex;
    justify-content: center;
    padding: 30px 0;
    border-bottom: 1px solid lightgrey;
}

.subreddit-list li {
    border: 1px solid green;
    border-radius: 2px;
    color: green;
    padding: 2px;
    margin: 0 2px;
    list-style: none;
}

.subreddit-list li span {
    color: grey;
}
.subreddit-list li span:hover {
    color: red;
    cursor: pointer;
}

.subreddit-list .empty {
    color: grey;
    height: 24px;
}

</style>