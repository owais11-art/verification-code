<script setup>
    defineProps(['isDisabled'])
    const emit = defineEmits(['validateCode'])
    const handleClick = () => emit('validateCode')
</script>

<template>
    <div class="btn">
        <button 
            @click="handleClick"
            :class="{disable: isDisabled}" 
            :disabled="isDisabled">VERIFICATION CODE</button>
    </div>
</template>

<style scoped lang="less">
    .btn{
        padding: 0 20px;
        margin-top: 20px;
        text-align: center;
        button{
            border: none;
            color: #fff;
            background: linear-gradient(93.32deg, #8D9EFF -10.93%, #A674FB 113.82%);
            width: 100%;
            padding: 10px 0;
            border-radius: 6px;
            cursor: pointer;
            &.disable{
                cursor:not-allowed;
            }
        }
    }
</style>