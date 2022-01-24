<template>
    <div class="app-card">
        <h3 class="card-title">Comments</h3>
        <div class="card-content">
            <div class="comments-table-box">
                <table class="comments-table">
                    <thead>
                    <tr>
                        <th @click="itemsSort('id')" class="is-sort-column" :data-sorted="sort_direction">ID</th>
                        <th>Name</th>
                        <th>Email</th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr v-for="item in itemsList" :key="item.id" @click="$router.push(`/comment/${item.id}`)">
                        <td>{{ item.id }}</td>
                        <td>{{ item.name }}</td>
                        <td>{{ item.email }}</td>
                    </tr>
                    </tbody>
                </table>
            </div>

            <pagination :page="page" :pages-count="pagesCount" @change="changePage"/>
        </div>
    </div>
</template>

<script>
export default {
    name: "CommentsTable",
    props: {
        items: {
            type: Array,
            default:() => ([]),
        },
    },
    data: () => ({
        page: 1,
        view_count: 10,
        sort_by: 'id',
        sort_direction: 'asc',
    }),
    methods: {
        itemsSort(sortBy) {
            this.sort_by = sortBy;
            this.sort_direction === 'asc' ? this.sort_direction = 'desc' : this.sort_direction = 'asc';
        },
        changePage(page) {
            this.page = page;
        },
    },
    computed: {
        pagesCount() {
            return Math.round(this.items.length / this.view_count);
        },
        sortedItems() {
            return this.items.sort((a, b) => this.sort_direction === 'asc' ? a[this.sort_by] - b[this.sort_by] : b[this.sort_by] - a[this.sort_by]);
        },
        itemsList() {
            return [...this.sortedItems].splice((this.page - 1) * this.view_count, this.view_count)
        },
    },
}
</script>