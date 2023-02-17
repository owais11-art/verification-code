<script setup>
    import checkmark from '../assets/checkmark.svg'
</script>
<template>
    <div class="verified">
        <div class="icon">
            <img :src="checkmark" alt="checkmark-icon">
        </div>
        <h2>VERIFIED</h2>
    </div>
</template>

<style scoped lang="less">
    .verified{
        height: 300px;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        gap: 20px;
        @media(max-width: 500px){
            width: 300px;
        }
        .icon{
            width: 80px;
            height: 80px;
            img{
                width: 100%;
                height: auto;
            }
        }
        h2{
            color: #6778E8
        }
    }
</style>