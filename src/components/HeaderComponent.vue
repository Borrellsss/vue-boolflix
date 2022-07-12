<template>
    <header>
        <div class="container">
            <div class="flex">
                <div class="logo">
                    <h2>BOOLFLIX</h2>
                </div>
                <div class="search">
                    <input type="text" v-model="title" placeholder="Search">
                    <button @click="$emit('axiosFilmsCall', title), $emit('axiosSeriesCall', title)">Search</button>
                </div>
            </div>
        </div>
    </header>
</template>

<script>
export default {
    name: "HeaderComponent",
    data() {
        return {
            title: "",
        }
    }
}
</script>

<style lang="scss" scoped>
// *IMPORTS
@import "../style/variables.scss";

// *STYLING
header {
    height: $header-height;
    background-color: #000;

    .container {

        .flex {
            height: $header-height;
            justify-content: space-between;
            align-items: center;
        }
    }
}
</style>