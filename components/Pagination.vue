<template>
    <div class="pagination-box">
        <ul class="pagination-list">
            <li key="prev">
                <a href="#" class="page-nav-btn" :class="{disabled: page === 1}"
                   @click.prevent="$emit('change', page > 1 ? page + -1 : 1)">Prev</a>
            </li>
            <li v-for="i in pagesCount" :key="i">
                <a v-if="itemType(i) === 'page'" :href="`#${i}`" :class="{ active: page === i }"
                   @click.prevent="$emit('change', i)">{{ i }}</a>
                <span v-else-if="itemType(i) === 'dot'" class="page-dots">...</span>
            </li>
            <li key="next">
                <a href="#" class="page-nav-btn" :class="{disabled: page === pagesCount}"
                   @click.prevent="$emit('change', page < pagesCount ? page + 1 : pagesCount)">Next</a>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "Pagination",
    props: {
        page: {
            type: Number,
            default: 1,
        },
        pagesCount: {
            type: Number,
            default: 0,
        },
    },
    data: () => ({
        has_dot: false,
    }),
    methods: {
        itemType(i) {
            if ([1, 2].indexOf(i) >= 0) return "page";
            if (i < this.page - 1 && i > this.page - 3) return 'dot';
            if (i >= this.page - 1 && i <= this.page + 1) return 'page';
            if (i > this.page + 1 && i < this.page + 3 && i < this.pagesCount - 1) return 'dot';
            if (i >= this.pagesCount - 1) return 'page';
            return false;
        },
    },
}
</script>