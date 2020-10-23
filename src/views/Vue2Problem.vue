<script>
import { ref } from "vue";
export default {
    setup() {
        const msg = ref("Hello World");

        return {
            msg
        };
    },
    render() {
        return (
            <p>
                1. vue2.0 所有的业务数据和逻辑都放在 data 和 methods 里面，代码组织混乱，不方便复用逻辑和阅读。<br/><br/>

                2. Vue3.0六大亮点<br/>
                    - Performance：性能比Vue 2.x快1.2~2倍<br/>
                    - Tree shaking support：按需编译,体积比Vue2.x更小<br/>
                    - Composition API: 组合API(类似React Hooks)<br/>
                    - Better TypeScript support：更好的 Ts 支持<br/>
                    - Custom Renderer API：暴露了自定义渲染API<br/>
                    - Fragment, Teleport(Protal), Suspense：更先进的组件<br/><br/>

                3. Vue3.0是如何变快的?<br/>
                    - diff算法优化: https://vue-next-template-explorer.netlify.app/<br/>
                        &nbsp;&nbsp;&nbsp;&nbsp;+ Vue2中的虚拟dom是进行全量的对比<br/>
                        &nbsp;&nbsp;&nbsp;&nbsp;+ Vue3新增了静态标记(PatchFlag),<br/>
                        在与上次虚拟节点进行对比时候，只对比带有patch flag的节点<br/>
                        并且可以通过flag的信息得知当前节点要对比的具体内容<br/>
                    - hoistStatic 静态提升<br/>
                        &nbsp;&nbsp;&nbsp;&nbsp;+ Vue2中无论元素是否参与更新, 每次都会重新创建, 然后再渲染<br/>
                        &nbsp;&nbsp;&nbsp;&nbsp;+ Vue3中对于不参与更新的元素, 会做静态提升, 只会被创建一次, 在渲染时直接复用即可<br/>
                    - cacheHandlers 事件侦听器缓存<br/>
                        &nbsp;&nbsp;&nbsp;&nbsp;+ 默认情况下onClick会被视为动态绑定, 所以每次都会去追踪它的变化<br/>
                        但是因为是同一个函数，所以没有追踪变化, 直接缓存起来复用即可<br/>
                    - ssr渲染<br/>
                        &nbsp;&nbsp;&nbsp;&nbsp;+ 当有大量静态的内容时候，这些内容会被当做纯字符串推进一个buffer里面，<br/>
                        即使存在动态的绑定，会通过模板插值嵌入进去。这样会比通过虚拟dmo来渲染的快上很多很多。<br/>
                        &nbsp;&nbsp;&nbsp;&nbsp;+ 当静态内容大到一定量级时候，会用_createStaticVNode方法在客户端去生成一个static node，<br/>
                        这些静态node，会被直接innerHtml，就不需要创建对象，然后根据对象渲染。<br/>
            </p>
        );
    },
};
</script>