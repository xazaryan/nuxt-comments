<template>
    <section>
        <div class="container">
            <comments-table :items="comments"/>
        </div>
    </section>
</template>

<script>
export default {
    name: 'IndexPage',
    data: () => ({
        comments: [],
    }),
    async fetch() {
        await this.$axios.$get('/comments')
            .then(comments => this.comments = comments)
    },
}
</script>
