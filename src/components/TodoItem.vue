<template>
    <div class="todo-item">
        <h3>{{todo.title}}</h3>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"]
}
</script>

<style scoped>
    .todo-item{
        background: #f4f4f4;
        border-bottom: solid 1px rgb(196, 196, 196);
    }
</style>