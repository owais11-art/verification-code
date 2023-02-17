<script setup>
    import { ref } from 'vue';

    const props = defineProps(['data'])
    const emit = defineEmits(['updateData'])
    const inputs = ref([])
    const digits = ref(props.data)
    const handleInput = (event, id) => {
        let val = event.target.value
        let next = null
        if(event.target.value.length>1){
            next = event.target.value[1]
            event.target.value = event.target.value[0]
            val = event.target.value[0]
        }
        if(event.inputType === 'deleteContentBackward') return
        let enableFocus = false
        digits.value = digits.value.map((digit, idx, array) => {
            if(enableFocus){
                inputs.value[idx].focus()
                next && (digit.val = next)
                enableFocus = false
            }
            if(digit.id === id){
                digit.val = val
                enableFocus = true
                if(idx === array.length-1) {
                    inputs.value[idx].blur()
                    emit('updateData', digits)
                }
            }
            return digit
        })
    }
</script>

<template>
    <div class="inputs">
        <input 
            type="text" 
            :class="{input: 'input', error: digit.error}"
            v-for="digit in digits"
            :key="digit.id"
            :value="digit.val"
            :id="{error: digit.error}"
            @input="(e) => handleInput(e, digit.id)"
            ref="inputs"
        />
    </div>
</template>

<style scoped lang="less">
    .inputs{
        margin-top: 20px;
        padding: 0 60px;
        display: flex;
        justify-content: center;
        gap: 20px;
        height: 70px;
        @media(max-width: 500px){
            padding: 0 10px;
        }
        .input{
            text-align: center;
            width: 25%;
            background-color: #F0F3FA;
            color: #6778E8;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            font-weight: 700;
            border: none;
            border-radius: 6px;
            outline: none;
            &.error{
                outline: 2px solid red;
            }
        }
    }
</style>