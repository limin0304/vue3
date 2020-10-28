<template>
    <!-- <p>{{ state.a }}</p>
    <p>{{ state.gf.b }}</p>
    <p>{{ state.gf.f.c }}</p>
    <p>{{ state.gf.f.s.d }}</p> -->
    <button @click="myFn">按钮</button>
</template>
<script>
/*
1.shallowReactive, shallowRef
2.shallowReadonly
3.reactive, ref
4.readonly
* */
export default {
    setup() {
        let obj = {
            a: "a",
            gf: {
                b: "b",
                f: {
                    c: "c",
                    s: {
                        d: "d",
                    },
                },
            },
        };

        let state = shallowReactive(obj);
        

        function myFn() {
            state.a = "1";
            state.gf.b = "2";
            state.gf.f.c = "3";
            state.gf.f.s.d = "4";

            console.log(state);
            // console.log(state.gf);
            // console.log(state.gf.f);
            // console.log(state.gf.f.s);
        }

        // let state = shallowRef(obj);
        // function myFn() {
        //     state.value.a = "1";
        //     state.value.gf.b = "2";
        //     state.value.gf.f.c = "3";
        //     state.value.gf.f.s.d = "4";
        //     console.log(state);
        //     console.log(state.value);
        //     console.log(state.value.gf);
        //     console.log(state.value.gf.f);
        //     console.log(state.value.gf.f.s);
        // }

        return { myFn, state };
    },
};

function shallowReactive(obj) {
    return new Proxy(obj, {
        get(obj, key) {
            // console.log(obj, key);
            return obj[key];
        },
        set(obj, key, val) {
            console.log(obj, key, val);
            obj[key] = val;
            console.log("更新UI界面");
            return true;
        },
    });
}

function shallowRef(val) {
    return shallowReactive({ value: val });
}

function reactive(obj) {
    if (Object.prototype.toString.call(obj) === '[object Object]' || obj instanceof Array) {
        for(let i in obj) {
            obj[i] = reactive(obj[i])
        }
        return shallowReactive(obj);
    } else {
        return shallowRef(obj);
    }
}

function ref(val) {
    return reactive({ value: val });
}

function shallowReadonly(obj) {
    return new Proxy(obj, {
        get(obj, key) {
            return obj[key];
        },
        set(obj, key, val) {
            console.log(obj, key, val);
            // obj[key] = val;
            console.log("只读的");
            return true;
        },
    });
}

function readonly(obj) {
    if (Object.prototype.toString.call(obj) === '[object Object]' || obj instanceof Array) {
        for(let i in obj) {
            obj[i] = readonly(obj[i])
        }
        return shallowReadonly(obj);
    }
    return shallowReadonly({ value: obj });
}

</script>


