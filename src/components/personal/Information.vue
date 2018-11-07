<template>
  <div>
    <Header></Header>
    <div class="row">
      <div class="col-lg-3"></div>
      <div class="col-lg-6 main-body row">
        <div class="col-lg-12 main-body-top font">
          <div><router-link to="/mycourse">我的课程</router-link></div>
          <div><router-link to="/mycollect">我的收藏</router-link></div>
          <div><router-link class="myinformation" to="/information">基本资料</router-link></div>
        </div>
        <div class="col-lg-12 main-body-bottom">
          <div>
            <button type="button" class="button-info"  @click="toggle1">
              基本信息
            </button>
          </div>
          <transition name="fade" >
            <div class="aaa " v-show="aaa">
              <div class="q_a clearfix">
                <div>
                  <div ><img src="../../assets/Personal/昵称.svg" alt="">&nbsp&nbsp昵称：</div><div>{{name}}</div>
                </div>
              </div>
              <div class="q_a clearfix">
                <div v-if="1" v-model="sex"><div><img src="../../assets/Personal/性别.svg" alt="">&nbsp&nbsp性别：</div><div>霹雳小美女</div></div>
                <div v-if="0" v-model="sex"><div><img src="../../assets/Personal/性别.svg" alt="">&nbsp&nbsp性别：</div><div>无敌大帅哥</div></div>
              </div>
              <div class="q_a clearfix">
                <div>
                  <div ><img src="../../assets/Personal/年龄.svg" alt="">&nbsp&nbsp年龄：</div><div>{{age}}岁</div>
                </div>
              </div>
              <div class="q_a clearfix">
                <div>
                  <div><img src="../../assets/Personal/身高.svg" alt="">&nbsp;&nbsp;身高：</div><div>{{height}}cm</div>
                </div>
              </div>
              <div class="q_a clearfix">
                <div>
                  <div><img src="../../assets/Personal/体重.svg" alt="">&nbsp;&nbsp;体重：</div><div>{{weight}}kg</div>
                </div>
              </div>
            </div>
          </transition>

          <div>
            <button type="button" class="button-address" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" @click="toggle2">
              收货地址
            </button>
          </div>
          <transition name="fade">
            <div class="bbb" v-show="bbb">
              <div class="q_a address clearfix"  :data-address-id="al.id" v-for="al in address_list">
                <div>
                  <div><img src="../../assets/Personal/姓名.svg" alt="">&nbsp;&nbsp;姓名：</div>
                  <div>{{al.recievename}}</div>
                </div>
                <div>
                  <div><img src="../../assets/Personal/电话.svg" alt="">&nbsp;&nbsp;手机号：</div>
                  <div>{{al.telephone}}</div>
                </div>
                <div class="address_span">
                  <div><img src="../../assets/Personal/地址.svg" alt="">&nbsp;&nbsp;地址：</div>
                  <div>{{al.province}}</div>
                  <div>{{al.city}}</div>
                  <div>{{al.area}}</div>
                  <span>{{al.detailaddress}}</span>
                  <!--<input class="checkbox" type="checkbox">-->
                  <input class="delete" type="button" @click="deladdress" value="删除">
                </div>
              </div>
            </div>
          </transition>

          <!--<div>-->
            <!--<button type="button" class="button-logistics" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" @click="toggle3">-->
              <!--待付款-->
            <!--</button>-->
          <!--</div>-->
          <!--<transition  name="fade" >-->
            <!--<div class="ccc" v-show="ccc" >-->
              <!--<div class="q_a pay clearfix" v-for="order1 in order1_list" :data-order1-id="order1.order_id" >-->
                <!--<div class="img" :style="{backgroundImage: 'url(' + order1.good_url + ')' } ">-->
                  <!--<img src="../../assets/Personal/删除黑.svg" alt="" style="width: 20px;height: 20px" @click="delorder1">-->
                <!--</div>-->
                <!--<div class="box">-->
                  <!--<div class="good_info">{{order1.good_name}}</div>-->
                  <!--<div class="price">￥{{order1.order_total}}</div>-->
                  <!--<span>共 {{order1.order_goodcounts}} 件</span>-->
                <!--</div>-->
                <!--<div class="payment" @click="dealorder1">立即付款</div>-->
              <!--</div>-->
            <!--</div>-->
          <!--</transition>-->

          <!--<div>-->
            <!--<button type="button" class="button-wait" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" @click="toggle4">-->
              <!--已付款-->
            <!--</button>-->
          <!--</div>-->
          <!--<transition  name="fade" >-->
            <!--<div class="ddd" v-show="ddd" >-->
              <!--<div class="q_a pay clearfix" v-for="order2 in order2_list" :data-order2-id="order2.order_id" >-->
                <!--<div class="img" :style="{backgroundImage: 'url(' + order2.good_url + ')' } ">-->
                  <!--<img src="../../assets/Personal/删除黑.svg" alt="" style="width: 20px;height: 20px" @click="delorder2">-->
                <!--</div>-->
                <!--<div class="box">-->
                  <!--<div class="good_info">{{order2.good_name}}</div>-->
                  <!--<div class="price">￥{{order2.order_total}}</div>-->
                  <!--<span>共 {{order2.order_goodcounts}} 件</span>-->
                <!--</div>-->
                <!--<div class="payment" @click="dealorder2">再来一单</div>-->
              <!--</div>-->
            <!--</div>-->
          <!--</transition>-->

          <div class="col-lg-3"></div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
  import Header from './top'
  import axios from 'axios'
  import $ from 'jquery'

export default {
  name: 'information',
  components:{Header},
  data(){
    return{
      name:'',
      sex:'0',
      age:'',
      height:'',
      weight:'',
      address_list:[],
      order1_list:[],
      order2_list:[],
      order_id:'',
      id:'',

      aaa:true,
      bbb:false,
      ccc:false,
      ddd:false,
      eee:false,
    }
  },
  created:function(){
    this.basic();
    this.address();
    this.getorder1();
    this.getorder2();
    this.$emit('flushnav')
  },
  methods:{
    basic:function(){
      let token=window.sessionStorage.getItem('token');
      let data1={
        headers:{"token":token}
      };
      let vm=this;
      if(token){
        axios({
          method:"POST",
          data:data1,
          url:this.GLOBAL.HOST+'user/getuserinfobytel/'
        })
          .then(function (response) {
            // console.log(response.data)
            vm.name=response.data[0].name;
            vm.sex=response.data[0].sex;
            vm.age=response.data[0].age;
            vm.height=response.data[0].height;
            vm.weight=response.data[0].width;
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    address:function(){
      let token=window.sessionStorage.getItem('token');
      let data1={
        headers:{"token":token}
      };
      let vm=this;
      if(token){
        axios({
          method:"POST",
          data:data1,
          url:this.GLOBAL.HOST+'user/getaddress/'
        })
          .then(function (response) {
            vm.address_list=response.data['data'];

          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    deladdress:function(e){
      let $obj = $(e.target).parents('.address')
      let i=$obj.attr('data-address-id')
      if (i){
        this.id=i
      }else {
        console.log('null id')
      }
      let vm=this;
      let token=window.sessionStorage.getItem('token');
      let data1={
        headers:{"token":token},
        "id":vm.id,
      };
      // console.log(data1)
      if(token){
        axios({
          method:"POST",
          data:data1,
          url:this.GLOBAL.HOST+'user/deladdress/'
        })
          .then(function (response) {
            vm.address();
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    getorder1:function(){
      let token=window.sessionStorage.getItem('token');
      let data1={
        token:token,
        good_status:'1'
      };
      let vm=this;
      if(token){
        axios({
          method:"POST",
          data:data1,
          url:this.GLOBAL.HOST+'shop/gettorder/'
        })
          .then(function (response) {
            vm.order1_list=response.data;
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    delorder1: function (e) {
      let vm = this;
      let $obj = $(e.target).parents('.pay')
      let id = $obj.attr('data-order1-id')
      if (id) {
        vm.order_id = id
      } else {
        console.log('null id')
      }
      let token = window.sessionStorage.getItem('token');
      let data1 = {
        token: token,
        "order_id": vm.order_id,
      };
      if (token) {
        axios({
          method: "POST",
          data: data1,
          url: this.GLOBAL.HOST + 'shop/delorder/'
        })
          .then(function (response) {
            console.log(response.data)
            vm.getorder1();
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    dealorder1: function (e) {
      let vm = this;
      let $obj = $(e.target).parents('.pay')
      let id = $obj.attr('data-order1-id')
      if (id) {
        vm.order_id = id
      } else {
        console.log('null id')
      }
      let token = window.sessionStorage.getItem('token');
      let data1 = {
        token: token,
        "order_id": [vm.order_id],
        "address_id":10,
      };
      if (token) {
        axios({
          method: "POST",
          data: data1,
          url: this.GLOBAL.HOST + 'shop/dealorder/'
        })
          .then(function (response) {
            // console.log(response.data)
            vm.getorder1();
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    getorder2:function(){
      let token=window.sessionStorage.getItem('token');
      let data1={
        token:token,
        good_status:'2'
      };
      let vm=this;
      if(token){
        axios({
          method:"POST",
          data:data1,
          url:this.GLOBAL.HOST+'shop/gettorder/'
        })
          .then(function (response) {
            vm.order2_list=response.data;
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    delorder2: function (e) {
      let vm = this;
      let $obj = $(e.target).parents('.pay')
      let id = $obj.attr('data-order2-id')
      if (id) {
        vm.order_id = id
      } else {
        console.log('null id')
      }
      let token = window.sessionStorage.getItem('token');
      let data1 = {
        token: token,
        "order_id": vm.order_id,
      };
      if (token) {
        axios({
          method: "POST",
          data: data1,
          url: this.GLOBAL.HOST + 'shop/delorder/'
        })
          .then(function (response) {
            // console.log(response.data)
            vm.getorder2();
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    dealorder2: function (e) {
      let vm = this;
      let $obj = $(e.target).parents('.pay')
      let id = $obj.attr('data-order2-id')
      if (id) {
        vm.order_id = id
      } else {
        console.log('null id')
      }
      let token = window.sessionStorage.getItem('token');
      let data1 = {
       token: token,
        "order_id":[ vm.order_id],
        "address_id":10,
      };
      if (token) {
        axios({
          method: "POST",
          data: data1,
          url: this.GLOBAL.HOST + 'shop/dealorder/'
        })
          .then(function (response) {
            vm.getorder2();
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    },
    toggle1:function () {
      var vm = this;
      vm.aaa=!vm.aaa;
    },
    toggle2:function () {
      var vm = this;
      vm.bbb=!vm.bbb;
    },
    toggle3:function () {
      var vm = this;
      vm.ccc=!vm.ccc;
    },
    toggle4:function () {
      var vm = this;
      vm.ddd=!vm.ddd;
    },

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  body{
    background:#f3f3f3;
    overflow-x:hidden;
  }
  .row{
    padding: 0px;
    margin: 0px;
  }
  .fade-enter-active, .fade-leave-active {
    max-height: 500px;
    min-height: 0px;
    overflow: hidden;
    transition: max-height ease-in .5s;
  }
  .fade-enter, .fade-leave-to {
    max-height: 0px;
    min-height: 0px;
    overflow: hidden;
    transition: max-height ease-out .5s;
  }

  .main-body{
    background: white;
    margin-top: 20px;
    border: solid 1px lightgray;
  }
  .main-body-top{
    height: 70px;
    margin: auto;
    border-bottom: solid 1px lightgray;
    display: flex;
    justify-content: space-around;
    line-height: 70px;
  }
  .main-body-top div{
    float: left;
    display: flex;
    justify-content: space-around;
  }
  .font{
    font-size: 18px;
    font-weight: 300;
  }
  .main-body-bottom {
    min-height:500px;
    +height:100%;
    _height:400px;
    margin: 0;
    padding: 0;
  }
  .myinformation{
    font-size: 20px;
    color: #584f60;
    font-weight: 500;
    border-bottom: solid 3px #584f60;
  }
  a{
    color: black !important;
  }
  a:hover{
    text-decoration: none;
  }
  /*----------------------------------个人信息部分----------------------------*/

  button{
    width: 100% !important;
    height: 40px;
    border: solid 1px lightgray;
    background: #f3f3f3;
    outline: none;
    font-size: 16px;
  }
  .q_a div{
    float: left;
    font-size: 17px;
    color: black;
    padding: 5px 0px 10px 35px;
  }
  .q_a img{

    width: 25px;
    height: 25px;
  }
  /*---------------------------收货地址-----------------------*/
  .address{
    /*background: gray;*/
    margin-top: 20px;
  }
  .address div{
    padding:5px 0px 0px 10px !important;
  }
  .address img{
    margin-left: 50px;
  }
  .bbb div{
    padding-bottom: 30px;
  }
  .address_span{
    width: 690px;
  }
  .address_span span{
    width: 450px;
    display:inline-block;
    padding-left:10px !important;
  }
  /*.address_span .checkbox{*/
    /*width: 18px;*/
    /*height: 18px;*/
    /*float: right;*/
    /*margin-top: -40px;*/
  /*}*/
  .address_span .delete{
    width: 50px;
    height: 30px;
    margin-top: -30px;
    float: right;
    border: solid 1px darkgray;
    border-radius: 3px;
    outline: none;
  }
  /*---------------------------待付款，已付款-------------------------*/
  .good_info{
    font-size: 14px !important;
    width: 350px;
  }
  .price{
    color: #ff2223 !important;
  }
  .box{
    width: 460px;
    font-size: 14px !important;
  }
  .box span{
    margin-left: 10px;
  }
  .pay{
    min-height: 100px;
  + height: 100 %;
    _height: 100px;
    margin: 15px 0 20px 30px;
  }
  .img img{
    display: none;
  }
  .pay:hover .img img{
    display: block;
  }
  .img{
    background-size: cover;
    border: solid 1px lightgray;
    width: 120px;
    height: 100px;
  }
  .pay div{
    padding:10px 15px 10px 10px !important;
  }
  .payment{
    width: 90px;
    height: 40px;
    background: red;
    margin-top: 25px;
    text-align: center;
    line-height: 25px;
    border-radius: 3px;
    font-size: 14px !important;
  }

  /*-----------------------------已发货-----------------------*/
  .number div{
    padding:0 15px 15px 0 !important;
    margin-top: -30px;
  }

</style>
