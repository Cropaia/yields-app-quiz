<template>
    <div class="nav">
        <slot></slot>
    </div>
</template>

<script>
export default {}
</script>

<style>
@media screen and (min-width: 500px) {
    .nav {
        width: 50rem;
    }
}

@media screen and (max-width: 499px) {
    .nav {
        left: 0;
        right: 0;
        padding-left: 3px;
        padding-right: 3px;
    }
}

.nav {
    position: fixed;
    z-index: 1000;
    top: 0;
    background-color: white;
    border-bottom: 1px solid black;
    margin: 0;
    padding-top: 3px;
    padding-bottom: 3px;
}
</style>
