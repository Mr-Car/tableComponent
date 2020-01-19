<template>
    <div class="container">
        <div id="tableBox" :style="'width:' + width + 'px;height:' + height + 'px;'">
            <div id="tableBox1">
                <table id="tableHead">
                    <tr>
                        <th
                            v-for="(item,index) in header"
                            :key="index"
                            :style="'width:' + item.width + 'px'"
                        >{{ item.prop }}</th>
                    </tr>
                </table>
            </div>
            <div id="tableBox2">
                <div id="left-div">
                    <!-- <div id="left-div1">
                        <table>
                            <tr>
                                <th :style="'height:'+ 50*n +'px'">编号</th>
                            </tr>
                        </table>
                    </div> -->
                    <div id="left-div2">
                        <table id="left-table2"></table>
                    </div>
                </div>
                <table id="right-table2">
                    <tr
                        v-for="( item, Itemindex ) in model"
                        :key="'row' + Itemindex"
                    >
                        <td
                            v-for="( headerItem, headerIndex ) in header"
                            :key="'col' + headerIndex"
                            :style="'width:' + headerItem.width + 'px'"
                        >{{ item[ headerItem.prop ] }}</td>
                    </tr>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
import $ from "jquery";
export default {
    props: {
        n: {
            type: Number
        },
        model: {
            type: Array
        },
        header: {
            type: Array
        },
        width:{
          type: Number|String
        },
        height:{
          type: Number|String
        },
    },
    data() {
        return {
            m: 1,
            data: []
        };
    },
    watch: {
        n(newVal) {
            this.m = newVal;
        }
    },
    mounted() {
        //生成表格内容
        // let htmlLeft = '';
        // let htmlRight = '';
        // for (let i = 1; i <= 10; i++) {
        //     htmlLeft += '<tr>';
        //     htmlLeft += '<td>' + i + '</td>';
        //     htmlLeft += '</tr>';
        // }
        // for (let i = 1; i <= 10; i++) {
        //     htmlRight += '<tr>';
        //     htmlRight += '<td>A</td>';
        //     htmlRight += '<td>100</td>';
        //     htmlRight += '<td>500</td>';
        //     htmlRight += '<td>1</td>';
        //     htmlRight += '<td>2</td>';
        //     htmlRight += '<td>3</td>';
        //     htmlRight += '<td>4</td>';
        //     htmlRight += '<td>5</td>';
        //     htmlRight += '</tr>';
        // }
        // $('#left-table2').html(htmlLeft);
        // $('#right-table2').html(htmlRight);
        //滚动
        // $('#tableBox2').on('scroll', function () {
        //     let top = $(this).scrollTop();// 获取当前滚动条上下滚动的距离
        //     let left = $(this).scrollLeft();//获取当前滚动条左右滚动的距离
        //     $('#left-div2').scrollTop(top);// 设置被选元素滚动条的垂直偏移
        //     $('#tableBox1').scrollLeft(left);//设置被选元素滚动条的水平偏移
        // })
        $("#tableBox2").scroll(function() {
            let top = $("#tableBox2").scrollTop();
            let left = $("#tableBox2").scrollLeft();
            $("#left-div2").scrollTop(top);
            $("#tableBox1").scrollLeft(left);
        });
        // 解决表头第一列与其他列高度不同步问题
        // let thHeight =  $("#tableBox1 th").height();
        // $("#left-div1 th").height(thHeight);
    }
};
</script>


<style lang="scss">
     * {
            margin: 0;
            padding: 0;
        }

        table {
            width: 100%;
            text-align: center;
            border-collapse: collapse;/*如果可能，边框会合并为一个单一的边框。*/
            border-spacing: 0;/*属性设置相邻单元格的边框间的距离*/
        }

        table td {
            word-break: break-all;/* word-break属性，可以让浏览器实现在任意位置的换行  break-all:允许在单词内换行 */
            word-wrap: break-word;/*在长单词或 URL 地址内部进行换行*/
        }

        .container {
            width: 500px;
            height: 500px;
            padding: 0;
            box-sizing: border-box;/*怪异盒*/
            margin: 50px auto 0;
        }

        #left-div {
            float: left;
        }

        #left-div1 {
            width: 100%;
        }

        #left-div2 {
            width: 100%;
            height: 250px;
            overflow: hidden;
        }
        /*滚动条占据了一定的位置，要把滚动条*/
        #left-table2 {
            margin-bottom: 4px;
        }

        #tableBox {
            /* float: left; */
            width: 340px;
        }

        #tableBox1 {
            width: 100%;
            overflow: hidden;
        }

        #tableBox2 {
            width: 100%;
            height: 250px;
            overflow: auto;/*这里设置auto是内容多了有滚动条，内容少了就不需要滚动条*/
        }

        #right-table2 {
            overflow: auto;
        }

        th,
        td {
            height: 50px;
            line-height: 50px;
            overflow: hidden;
            text-align: center;
        }

        th {
            color: #1E304F;
            background-color: #F3F8FF;
        }

        td {
            color: #384967;
        }

        tr:nth-of-type(odd) {
            background: #E7F2FF;
        }

        #tableBox2::-webkit-scrollbar {
            /*滚动条整体样式*/
            width: 4px;
            height: 4px;
        }

        #tableBox2::-webkit-scrollbar-thumb {
            /*滚动条里面小方块*/
            border-radius: 5px;
            box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
            background: rgba(0, 0, 0, 0.2);
        }

        #tableBox2::-webkit-scrollbar-track {
            /*滚动条里面轨道*/
            box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
            border-radius: 0;
            background: rgba(0, 0, 0, 0.1);
        }
</style>