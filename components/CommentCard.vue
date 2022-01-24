<template>
    <div class="app-card">
        <h3 class="card-title">Comment #{{ comment.id }}</h3>
        <div class="card-content">
            <ul class="comment-more-info-list">
                <li v-for="(val, key) in comment">
                    <span>{{ key }}:</span>
                    <strong>{{ val }}</strong>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: "CommentCard",
    props: {
        comment: {
            type: Object,
            required: true,
        },
    },
}
</script>