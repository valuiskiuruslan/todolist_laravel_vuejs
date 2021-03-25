<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item
                :item="item"
                class="item"
                @itemChanged="$emit('reloadList')"
            />
        </div>
    </div>
</template>

<script>
    import listItem from "./listItem";

    export default {
        name: "listView",
        props: [
            "items"
        ],
        components: {
            listItem
        }
    }
</script>

<style scoped>
    .item {
        margin-top: 5px;
        padding: 5px;
        background: #e6e6e6;
    }
</style>
