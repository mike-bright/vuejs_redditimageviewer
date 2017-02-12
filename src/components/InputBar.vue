<template>
    <div class="input-bar">
        <span>/r/</span>
        <input
            type="text"
            v-model.trim="subreddit"
            :class="classObject"
            :placeholder="placeholder"
            @keyup.enter="subredditEntered">
    </div>
</template>

<script>
    export default {
        name: 'input-bar',
        data: function() {
            return {
                placeholder: 'enter a subreddit',
                subreddit: ''
            }
        },
        methods: {
            subredditEntered: function() {
                if (!this.hasError) {
                    this.$emit('subredditEntered', this.subreddit);
                    this.subreddit = "";
                }
            }
        },
        computed: {
            classObject: function() {
                return {
                    'has-error': this.hasError
                };
            },
            hasError: function() {
                return /([^a-zA-Z0-9\_])/.test(this.subreddit);
            }
        }
    }
</script>

<style scoped>
    .input-bar {
        display: flex;
        padding: 30px 0 0 0;
        justify-content: center;
        font-size: 15px;
        color: grey;
    }

    .input-bar span {
        padding: 5px;
    }

    .input-bar input {
        padding: 5px;
        min-width: 300px;
        color: grey;
    }
    .input-bar input.has-error {
        color: red;
    }
</style>