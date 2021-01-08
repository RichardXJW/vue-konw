<template>
    <div id="app">
        <table border="1px" cellspacing="0">
            <tr>
                <th>序号</th>
                <th>书籍名称</th>
                <th>出版日期</th>
                <th>价格</th>
                <th>购买数量</th>
                <th>操作</th>
            </tr>
            <tr v-for="(item, index) in books" :key="item">
                <td>{{index+1}}</td>
                <td>{{item.name}}</td>
                <td>{{item.time}}</td>
                <td>¥{{item.price.toFixed(2)}}</td>
                <td>
                    <button type="button" @click="subNum(index)">-</button>
                    {{item.nums}}
                    <button type="button" @click="addNum(index)">+</button>
                </td>
                <td>
                    <button type="button" @click="del(index)">删除</button>
                </td>
            </tr>
        </table>
        <div style="text-align: left">
            <label :for="total">总价格：</label><span>¥{{total.toFixed(2)}}</span>
        </div>
    </div>
</template>
<script>


    export default {
        name: 'App',
        // components: {},
        data() {
            return {
                books: [{
                    name: "算法导论",
                    time: "2006-9",
                    price: 85,
                    nums: 0,
                },
                    {
                        name: "《UNIX编程艺术》",
                        time: "2006-2",
                        price: 59,
                        nums: 0,
                    }, {
                        name: "《编程珠玑》",
                        time: "2008-10",
                        price: 39,
                        nums: 0,
                    }, {
                        name: "代码大全",
                        time: "2006-3",
                        price: 128,
                        nums: 0,
                    }]
            }
        },
        methods: {
            subNum(index) {
                if (this.books[index].nums <= 0) {
                    alert("购买数量不能小于0！");
                    return;
                }
                this.books[index].nums--;
            },
            addNum(index) {
                this.books[index].nums++;
            },
            del(index) {
                this.books.splice(index, 1);
            }
        },
        computed: {
            total(){
               let sum =  this.books.map(function (obj) {
                    return obj.nums * obj.price
                }).reduce(function (preValue, value) {
                    return preValue + value;
                }, 0);
               return sum;
            }
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
