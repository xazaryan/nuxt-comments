<template>
    <section>
        <div class="container">
            <comment-card :comment="comment"/>
        </div>
    </section>
</template>

<script>
export default {
    name: "CommentPage",
    data: () => ({
        comment: {
            postId: null,
            id: null,
            name: '',
            email: '',
            body: '',
        },
    }),
    async fetch() {
        await this.$axios.$get(`/comments/${this.$route.params.id}`)
            .then(comment => this.comment = comment)
    },
}
</script>