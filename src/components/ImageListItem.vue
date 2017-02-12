<template>
    <div class="image-list-item">
        <img :src="this.imageURL">
        <span>{{ this.post.data.title }} </span>
    </div>
</template>

<script>
    export default {
        name: 'image-list-item',
        props: ['post'],
        computed: {
            imageURL: function() {
                return this.post.data.url.replace(/&amp;/g, '&')
            }
        },
        mounted: function() {
            var self = this;
            this.$el.querySelector('img').onerror = function() {
                self.$emit('downloadFailed');
            };
        }
    }
</script>

<style scoped>
    .image-list-item {
        display: flex;
        flex-direction: column;
        align-items: center;
        min-width: 300px;
        padding: 5px;
        background: lightgrey;
        border: 1px solid darkgrey;
        border-radius: 5px;
        margin: 5px;
    }

    .image-list-item img {
        width: auto;
        height: auto;
        max-height: 500px;
    }

    .image-list-item span {
        margin-top: 5px;
    }
</style>