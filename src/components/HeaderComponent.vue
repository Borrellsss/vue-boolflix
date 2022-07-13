<template>
    <header>
        <div class="container">
            <div class="flex">
                <div class="logo">
                    <img src="../assets/img/boolflix-logo.png" alt="boolflix logo">
                </div>
                <div class="search">
                    <input @keyup.enter="$emit('axiosFilmsCall', title), $emit('axiosSeriesCall', title)" type="text" v-model="title" placeholder="Search">
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
    background-color: rgba(0, 0, 0, 0);
    transition: all 300ms;

    &:hover {
        background-color: #000;
        box-shadow: 0 0 10px #000;
    }
    .container {

        .flex {
            height: $header-height;
            justify-content: space-between;
            align-items: center;
        }
    }
}
</style>