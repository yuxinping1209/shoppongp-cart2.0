<template>
  <div class="hello">
    <table class="cart" align="center">
      <thead class="title">
        <td><input type="checkbox" v-model="checked" @click="toggle"> 全选</td>
        <td>商品</td>
        <td>单价</td>
        <td>数量</td>
        <td>金额</td>
        <td>操作</td>
      </thead>
      <tbody>
        <tr v-for="item in postList" :key=item.id>
          <td><input type="checkbox" :value="item.id" v-model="isSelect"></td>
          
          <td><div class="main"><img :src="item.pic" width=100 height=100>{{item.name}}</div></td>
          <td>{{item.price}}</td>
          <td><button  @click="item.count<=1?1:item.count--">-</button>{{item.count}}<button @click="item.count++">+</button></td>
          <td>{{item.price*item.count}}</td>
          <td><button @click="deleteOne">删除</button></td>
        </tr>
        <tr >
       
            <td class="no"><button @click="deleteAll">批量删除</button></td> 
            <td class="no"></td>
            <td class="no"></td>
            <td class="no"></td>
            <td class="no"><span>总计{{totalprices}}元</span></td>
            <td class="pay no">
              
              <button>结算</button>
              </td>
         
         
        </tr>
      </tbody>
     
        
      
        

    </table>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      postList:[{id:1,pic:require("../assets/logo.png"),name:"iphone",count:1,price:5000,prices:""},
                {id:2,pic:require("../assets/logo.png"),name:"ipad",count:1,price:3000,prices:""},
                {id:3,pic:require("../assets/logo.png"),name:"imac",count:1,price:8000,prices:""}],
      isSelect:[],
      checked:false
      
    }
  },
  computed:{
    totalprices(){
      let totalprices=0
      for (let index = 0; index < this.isSelect.length; index++) {
       let i= this.postList.map(item=>item.id).indexOf(this.isSelect[index])
       totalprices=totalprices+this.postList[i].count*this.postList[i].price
        
      }
      return totalprices
    }
  },
  methods:{
    toggle(){
      if(this.checked){
        console.log(this.isSelect)
        this.isSelect=[]
      }else{
        console.log(this.checked)
        this.postList.forEach(item=>{
          this.isSelect.push(item.id)
        })
      }
    },
    deleteOne(index){
      this.postList.splice(index,1)
      this.isSelect.splice(index,1)

    },
    deleteAll(){
      console.log(1)
      this.isSelect.forEach(item=>{
        let n=this.postList.map(item=>item.id).indexOf(item)
         console.log(this.postList)
        this.$set(this.postList[n],'selected',true)
        
      })
      this.postList=this.postList.filter((key)=>{return !key.selected})
      this.isSelect=[]  
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cart{
  width:80%;
  border:1px solid lightsteelblue;

}
td{
  border:1px solid lightsteelblue;
  vertical-align: center;
}
.main{
  display:flex;
  align-items: center;
  justify-content: center;
}
.foot{
  display:flex;
  justify-content: space-between;
  padding:5px 10px;
  border:1px solid red;
}
.no{
  border:none;
}
</style>
