<template>
    <div>
        <p>{{ age }}</p>
        <p>{{ state.name }}</p>
    </div>
</template>

<script>
import { ref, reactive, watch } from "vue";
export default {
    name: "App",
    setup() {
        let age = ref(18);

        watch(age, (current, prev) => {
            console.log('当前：', current);
            console.log('之前：', prev);
        });

        let state = reactive({
            name: '小明'
        });
        
        // watch(() => state.name, (current, prev) => {
        //     console.log('当前：', current);
        //     console.log('之前：', prev);
        // });

        // watch([age, () => state.name], ([current, current2], [prev, prev2]) => {
        //     console.log('当前：', current, current2);
        //     console.log('之前：', prev, prev2);
        // })



        setTimeout(() => {
            age.value++;
            state.name = '小红';
        }, 100);

        return { age, state };
    },
};
</script>

<style>
</style>
