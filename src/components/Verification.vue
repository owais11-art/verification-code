<script setup>
    import { ref } from 'vue'
    import Verified from './Verified.vue'
    import Inputs from './Inputs.vue'
    import Button from './Button.vue'
    const data = ref([
        {
            id: 1,
            val: '',
            error: false
        },
        {
            id: 2,
            val: '',
            error: false
        },
        {
            id: 3,
            val: '',
            error: false
        },
        {
            id: 4,
            val: '',
            error: false
        }
    ])
    const isDisabled = ref(true)
    const isVerified = ref(false)
    const updateData = digits => {
        data.value = digits.value
        isDisabled.value = false
    }
    const validateCode = () => {
        let notHaveError = true
        data.value = data.value.map(item => {
            if(!item.val || !Number.isInteger(parseInt(item.val))) {
                item.error = true
                notHaveError = false
            }
            return item
        })
        if(notHaveError) isVerified.value = true
    }
</script>

<template>
    <main :class="{verified: isVerified}">
        <Verified v-if="isVerified"/>
        <template v-else>
            <h1>VERIFICATION CODE</h1>
            <p>Please enter the code that we sent to(***)***-2891</p>
            <Inputs
                :data="data"
                @update-data="updateData"
            />
            <Button
                :isDisabled="isDisabled"
                @validate-code="validateCode"
            />
        </template>
    </main>
</template>

<style scoped lang="less">
    main{
        width: 500px;
        background-color: #fff;
        box-shadow: 5px 5px 20px 0 rgba(0, 0, 0, 0.5);
        border-radius: 6px;
        padding: 30px 20px;
        &.verified{
            background-color: antiquewhite;
        }
        h1{
            color: #6778E8;
            text-align: center;
            font-weight: 700;
            font-size: 20px;
        }
        p{
            text-align: center;
            color: #444444;
            font-size: 15px;
            font-weight: 600;
            margin-top: 20px;
        }
        @media(max-width: 500px){
            width: 95%;
            margin: 0 auto;
        }
    }
</style>