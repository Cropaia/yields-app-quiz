<template>
    <div class="progress">
        <div class="progress-bar" :style="style">
            {{ value }} / {{ max }}
        </div>
    </div>
</template>

<script>
export default {
    props: ["value", "max"],
    computed: {
        style() {
            const percent = this.value / this.max * 100;
            return {
                "width": percent + "%"
            };
        }
    }
}
</script>

<style>
.progress {
    height: 3.2rem;
    overflow: hidden;
    background-color: #f5f5f5;
    border-radius: 4px;
    -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, .1);
            box-shadow: inset 0 1px 2px rgba(0, 0, 0, .1);
}
.progress-bar {
    float: left;
    width: 0;
    height: 100%;
    font-size: 1.4rem;
    line-height: 3.2rem;
    color: #fff;
    text-align: center;
    background-color: #fcac14;
    -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, .15);
            box-shadow: inset 0 -1px 0 rgba(0, 0, 0, .15);
    -webkit-transition: width .6s ease;
         -o-transition: width .6s ease;
            transition: width .6s ease;
}
</style>
