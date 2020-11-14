<template>
  <div class="layout">
      <div class="main"></div>
      <div class="product">
      
      </div>
      <div class="orders">
      <h3>Orders</h3>
      <div class="order-list">
       <div 
       class="list" 
       v-for="list in orderList" 
       :key="list.name"
      @click="list.quantity++"
        >
        <p>{{list.name}}</p>
        <p>{{list.pricePerUnit}}</p>
        <p>{{list.quantity}}</p>
        <p>{{list.quantity * list.pricePerUnit}}</p>
       </div>
      </div>
      <div class="total">
      <p>Total</p>
      <p>{{ getTotal }}</p>
      
      </div>
      <div class="button-group">
       <button class="btn" style="background-color: #5cb85c; color:white">Checkout</button>
      </div>

      </div>
  </div>
</template>


  <style scoped>
  .main{
  display: flex;
  flex-flow: 1;
  max-height: 100vh;
  }

  .orders{
    display: grid;
    grid-template-rows: 50px 1fr 50px 50px; /*แบ่งขนาดตามส่วน */
    margin-left: auto;
    min-width: 300px;
    padding: 10px;
    background-color: gray;
    color: aliceblue;
    gap :10px; /*กำหนดช่องว่าง*/
    /*align-items: center;*/
  
}

.orders h3 {
margin: 0;
}

    .total{
    display: flex; /*ชิดซขวา*/
    font-weight: bold;
    font-size: 20px;
    }
    .total > p { /* ตั้งแต่totalขึ้นไป*/
    margin:0;
    }
    .total > p:last-child{
    margin-left: auto;
    }

    .orders > h3 {
    margin: 0;
    }

    .button-group{
    display: flex;
    }
    .button-group > button{
    flex-grow: 1;
    }

    .orders-list{
    display: flex;
    flex-direction: column;
    gap: 10px;
    overflow-y: auto;
    overflow-x: hidden;
    }
    .list{
    display: grid;
    grid-template-columns: 1fr 50px 50px 50px;
    gap: 10px;
    }

    .list > p {
    margin: 0;
    }

    .list > p:not(:first-child){
    text-align: right;
    }

  </style>

<script>
export default {
name : "Home",
data(){
return {
    
      orderList:[
        {
          name : "Fish & Ship",
          quantity : 1,
          pricePerUnit: 220
        },
        {
          name : "Rice hot",
          quantity : 1,
          pricePerUnit: 203
        },
        {
          name : "Mama",
          quantity : 1,
          pricePerUnit: 240
        },
        {
          name : "Yamyam",
          quantity : 1,
          pricePerUnit: 201
        },
      ]
    }
  },


  computed: {
  getTotal(){
    const total = this.orderList.reduce(
      (prev,current)=> prev + (current.quantity * current.pricePerUnit),0);
    return new Intl.NumberFormat("th-TH",{
      style : "currency",
      currency : "THB"
      }).format(total);
    }
  },
};
</script>
