<template>
    <div class="card">
         <div v-if="selected" class="card-face">
             <img :src="`/images/${cardImage}.jpg`">
         </div>
         <div v-else class="card-back">
             <img src="/images/BackSide.png">
         </div>
    </div>
 
</template>

<script>
export default {
    props:{
        value: {

        },
        selected: {
            default: false
        },
        cardImage: {

        }
    },
    methods: {
  }

}
</script>

<style>
    @keyframes rotate {
        0% { opacity: 0; transform: rotateY(-180deg); }
        100% { opacity: 1; transform: rotateY(0deg); }
    }

    .card { 
        
    }
    .card-face {
        animation: rotate 1s;

    }
    .card-back {
        animation: rotate 1s reverse;
    }
    img {
        height: 230px;
        width: 180px;
    }

</style>