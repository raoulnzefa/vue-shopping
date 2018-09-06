<template>
    <div class="pos">
        <div>
            <el-row>
                <el-col :span='7' id="order-list" class="pos-order">
                    <el-tabs>
                        <el-tab-pane label="点餐">
                            <el-table :data="tableData" border style="width: 100%">

                                <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                                <el-table-column prop="count" label="量" width="50"></el-table-column>
                                <el-table-column prop="price" label="金额" width="70"></el-table-column>
                                 <!-- fixed="right" -->
                                <el-table-column label="操作" width="100"  fixed="right">
                                    <template slot-scope="scope">
                                        <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
                                        <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                                    </template>
                                </el-table-column>  

                            </el-table>
                            <div class="totalDiv">
                                <small>数量: </small>
                                <strong>{{totalCount}}</strong> &nbsp; &nbsp; &nbsp; &nbsp;
                                <small>总计: </small>
                                <strong>{{totalMoney}}</strong>元
                            </div>
                            <div class="div-btn">
                                <el-button type="warning">挂单</el-button>
                                <el-button type="danger"  @click="delAllGoods()">删除</el-button>
                                <el-button type="success"  @click="checkout()">结账</el-button>
                            </div>
                            
                        </el-tab-pane>
                        <el-tab-pane label="挂单">
                            挂单
                        </el-tab-pane>
                        <el-tab-pane label="外卖">
                            外卖
                        </el-tab-pane>
                    </el-tabs>
                   
                </el-col>
                <!-- 商品展示 -->
                <el-col :span='17' id="order-list">
                    <div class="often-goods">
                        <div class="title">常用商品</div>
                        <div class="often-goods-list">
                            <ul>
                                <li v-for="goods in oftenGoods" @click="addOrderList(goods)">
                                    <span>{{goods.goodsName}}</span>
                                    <span class="o-price">￥{{goods.price}}元</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div class="goods-type">
                         <el-tabs>
                            <el-tab-pane label="汉堡">
                                <ul class="cookList">
                                    <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width=100%></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                   </li>
                                </ul>
                                
                            </el-tab-pane>
                            <el-tab-pane label="小食">
                                <ul class="cookList">
                                    <li v-for="goods in type1Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width=100%></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="饮料">
                                <ul class="cookList">
                                    <li v-for="goods in type2Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width=100%></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="套餐">
                                <ul class="cookList">
                                    <li v-for="goods in type3Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width=100%></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                        </el-tabs>
                    </div>
                   
                </el-col>
            </el-row>
        </div>
    </div>
</template>

<script>
// import axios from 'axios'
export default {
    name: 'Pos',
    data () {
        return {
            totalCount: 0,
            totalMoney: 0,
            tableData: [],
            oftenGoods:[
                {
                    goodsId:1,
                    goodsName:'香辣鸡腿堡',
                    price:18
                }, {
                    goodsId:2,
                    goodsName:'田园鸡腿堡',
                    price:15
                }, {
                    goodsId:3,
                    goodsName:'和风汉堡',
                    price:15
                }, {
                    goodsId:4,
                    goodsName:'快乐全家桶',
                    price:80
                }, {
                    goodsId:5,
                    goodsName:'脆皮炸鸡腿',
                    price:10
                }, {
                    goodsId:6,
                    goodsName:'魔法鸡块',
                    price:20
                }, {
                    goodsId:7,
                    goodsName:'可乐大杯',
                    price:10
                }, {
                    goodsId:8,
                    goodsName:'雪顶咖啡',
                    price:18
                }, {
                    goodsId:9,
                    goodsName:'大块鸡米花',
                    price:15
                }, {
                    goodsId:20,
                    goodsName:'香脆鸡柳',
                    price:17
                }
            ],
            type0Goods:[
                {
                    goodsId:1,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
                    goodsName:'香辣鸡腿堡',
                    price:18
                }, {
                    goodsId:2,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                    goodsName:'田园鸡腿堡',
                    price:15
                }, {
                    goodsId:3,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                    goodsName:'和风汉堡',
                    price:15
                }, {
                    goodsId:4,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                    goodsName:'快乐全家桶',
                    price:80
                }, {
                    goodsId:5,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                    goodsName:'脆皮炸鸡腿',
                    price:10
                }, {
                    goodsId:6,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                    goodsName:'魔法鸡块',
                    price:20
                }, {
                    goodsId:7,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
                    goodsName:'可乐大杯',
                    price:10
                }, {
                    goodsId:8,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                    goodsName:'雪顶咖啡',
                    price:18
                }, {
                    goodsId:9,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                    goodsName:'大块鸡米花',
                    price:15
                }, {
                    goodsId:20,
                    goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                    goodsName:'香脆鸡柳',
                    price:17
                }
            ], 
            type1Goods:[
                {
                    goodsId:1,
                    goodsImg:"http://www.weirujia.com/uploads/allimg/1705/1-1F5032159330-L.jpg",
                    goodsName:'嫩牛五方',
                    price:17
                },
                {
                    goodsId:2,
                    goodsImg:"http://www.weirujia.com/uploads/allimg/1802/1-1P2060331440-L.jpg",
                    goodsName:'珍宝糯米翅',
                    price:18
                },
                 {
                    goodsId:3,
                    goodsImg:"http://www.weirujia.com/uploads/allimg/1709/1-1F930033230Z5.jpg",
                    goodsName:'小鲜肉薯饼',
                    price:15
                }
            ],
            type2Goods: [
                {
                    goodsId:1,
                    goodsImg:"http://www.weirujia.com/uploads/allimg/1803/1-1P30F454500-L.jpg",
                    goodsName:'猫咪咖啡',
                    price:17
                },
                {
                    goodsId:2,
                    goodsImg:"http://www.weirujia.com/uploads/allimg/1611/1-1611061920030-L.jpg",
                    goodsName:'玉米饮',
                    price:12
                },
                {
                    goodsId:3,
                    goodsImg:"http://www.weirujia.com/uploads/allimg/1709/1-1F91F109130-L.jpg",
                    goodsName:'拿铁豆浆',
                    price:10
                }
            ],
            type3Goods: [
                {
                    goodsId:1,
                    goodsImg:"http://www.weirujia.com/uploads/allimg/1705/1-1F522035451404.jpg",
                    goodsName:'超值全家桶',
                    price:17
                },
                {
                    goodsId:2,
                    goodsImg:"http://www.weirujia.com/uploads/allimg/1606/1-16063003402T55.jpg",
                    goodsName:'外带全家桶',
                    price:12
                }
            ],
        }
    },
    mounted: function () {
        var orderHeight = document.body.clientHeight;
        document.getElementById('order-list').style.height = orderHeight + 'px';
    },
     methods: {
        //添加订单列表的方法
        addOrderList(goods) {
            //console.log(goods);
            this.totalCount = 0; //汇总数量清0
            this.totalMoney = 0;
            let isHave = false;
            //判断是否这个商品已经存在于订单列表
            for (let i = 0; i < this.tableData.length; i++) {
                // console.log(this.tableData[i].goodsId);
                if (this.tableData[i].goodsId == goods.goodsId) {

                    isHave = true; //存在

                }
            }
            //根据isHave的值判断订单列表中是否已经有此商品
            if (isHave) {
                //存在就进行数量添加
                let arr = this.tableData.filter(o => o.goodsId == goods.goodsId);
                arr[0].count++;
                //console.log(arr);
            } else {
                //不存在就推入数组
                let newGoods = { goodsId: goods.goodsId, goodsName: goods.goodsName, price: goods.price, count: 1 };
                this.tableData.push(newGoods);

            }

            this.getAllMoney();
        },
        //删除单个商品
        delSingleGoods(goods) {
            // console.log(goods);
            this.tableData = this.tableData.filter(o => o.goodsId != goods.goodsId);
            this.getAllMoney();

        },
        //删除所有商品
        delAllGoods() {
            this.tableData = [];
            this.totalCount = 0;
            this.totalMoney = 0;
        },
        //汇总数量和金额
        getAllMoney() {
            this.totalCount = 0;
            this.totalMoney = 0;
            if (this.tableData) {
                this.tableData.forEach((element) => {
                    this.totalCount += element.count;
                    this.totalMoney = this.totalMoney + (element.price * element.count);
                });
            }
        },
        //结账方法模拟
        checkout() {
            if (this.totalCount!=0) {
                this.tableData = [];
                this.totalCount = 0;
                this.totalMoney = 0;
                this.$message({
                    message: '结账成功，感谢你又为店里出了一份力!',
                    type: 'success'
                });

            }else{
                this.$message.error('不能空结。老板了解你急切的心情！');

            }

        }


    }
}
</script>

<style scoped>
.pos {
    font-size: 13px;  
}
.pos-order {
    background-color: #F9FAFC;
    border-right: 1px solid #C0CCDA;
    height: 100%;
}
.div-btn {
    margin-top: 10px;
    text-align: center;
}
.title {
    height: 20px;
    font-size: 15px;
    border-bottom: 1px solid #D3DCE6;
    padding: 9px;
    background-color: #F9FAFC;
    text-align: left;
}

#order-list {
    border-left: 2px solid #E6E4E4;
}
.goods-type {
    clear: both;
    margin-left: 10px;
}
.often-goods-list ul li{
    list-style: none;
    float: left;
    border: 1px solid #E5E9F2;
    padding: 6px;
    margin: 5px;
    background: #fff;
}

.o-price{
      color:#58B7FF; 
   }
.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auto;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
   }
   .cookList li span{
        display: block;
        float:left;
   }
   .foodImg{
       width: 30%;
   }
   .foodName{
       font-size: 15px;
       padding-left: 10px;
       color:brown;
   }
   .foodPrice{
       font-size: 15px;
       padding-left: 10px;
       padding-top:10px;
   }
</style>
