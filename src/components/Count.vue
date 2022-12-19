<template>
  <div>
    <h1>当前求和为{{sum}}</h1>
    <h3>当前求和放大100倍是{{bigSum}}</h3>
    <h3>学校是{{school}}</h3>
    <h3 style="color: orange">Person组件的人数总数是{{personList.length}}</h3>
    <select v-model.number="n">
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
    </select>
    <button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementOdd(n)">若当前求和为奇数才加</button>
    <button @click="incrementWait(n)">等一等再加</button>
  </div>
</template>

<script>
    import {mapState, mapGetters, mapMutations, mapActions} from 'vuex'
    export default {
        name: 'Count',
        data() {
            return {
                n: 1, // 下拉栏默认选择的数字
            }
        },
        computed: {
            // 纯计算属性来简化模板数据
            // sum() {
            //     return this.$store.state.sum
            // },
            
            // school() {
            //     return this.$store.state.school
            // },

            // 利用mapState简化
            // ...mapState({sum: 'sum', school: 'school'}), //对象形式
            ...mapState(['sum', 'school', 'personList']), // 数组形式，共享数据新增personList

            // bigSum() {
            //     return this.$store.getters.bigSum
            // },
            // ...mapGetters({bigSum: 'bigSum'}), //对象形式
            ...mapGetters(['bigSum']) //数组形式
        },
        methods: {
            // increment() {
            //     // 没有业务逻辑需要处理的话，之间传给mutations操作数据即可
            //     this.$store.commit('JIA', this.n)
            // },
            // decrement() {
            //     this.$store.commit('JIAN', this.n)
            // },
            // mapMutations用的时候需要在模板中传参，因为不传参的话value是指event，无法计算
            ...mapMutations({increment: 'JIA', decrement: 'JIAN'}),
            // incrementOdd() {
            //     this.$store.dispatch('jiaOdd', this.n)
            // },
            // incrementWait() {
            //     this.$store.dispatch('jiaWait', this.n)
            // },
            // mapActions用法与mapMutations类似
            ...mapActions({incrementOdd: 'jiaOdd', incrementWait: 'jiaWait'})
        },
        mounted() {
            // console.log(this.$store);
        },
    }
</script>

<style>
    button {
        margin-left: 5px;
    }
</style>