<template>
  <div>
    <h1>人员列表</h1>
    <h3 style="color: orange">Count组件的当前求和为{{sum}}</h3>
    <input type="text" placeholder="请输入人员名称" v-model="name">
    <button @click="addPerson">添加</button>
    <ul>
        <li v-for="p in personList" :key="p.id">{{p.name}}</li>
    </ul>
  </div>
</template>

<script>
    import {nanoid} from 'nanoid'
    export default {
        name: 'Persons',
        data() {
            return {
                name: ''
            }
        },
        computed: {
            personList() {
                return this.$store.state.personList
            },
            sum() {
                return this.$store.state.sum
            }
        },
        methods: {
            addPerson() {
                const person = {id: nanoid(), name: this.name}
                this.$store.commit('ADD_PERSON', person)
                this.name = ''
            }
        }
    }
</script>
