<template>
    <div class="image-list">
        <image-list-item v-for="(post, index) in this.posts"
            :post="post"
            @downloadFailed="removePost(index)"
        ></image-list-item>
        <div v-if="!this.subreddits.length">
            <!-- images will appear here -->
        </div>
        <div v-else-if="!this.posts.length">
            loading...
        </div>
    </div>
</template>

<script>
    import ImageListItem from './ImageListItem'

    export default {
        name: 'image-list',
        components: {
            'image-list-item': ImageListItem
        },
        props: ['posts', 'subreddits'],
        methods: {
            removePost: function(index) {
                this.posts.splice(index, 1);
            }
        }
    }
</script>

<style scoped>
    .image-list {
        margin-top: 30px;
        color: grey;
        display: flex;
        flex-wrap: wrap;
        align-items: flex-start;
        justify-content: center;
    }
</style>