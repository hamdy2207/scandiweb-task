<template>
    <div class="container">
        <header>
            <div>
                <h2>Product Add</h2>
            </div>
             <div class="btns-header">                
                <button class="btn" @click="$store.commit('addProduct')" type="Submit">Save</button>

                <button class="btn" @click="$store.commit('back')">Cancel</button>
            </div>
        </header>
        <hr>
        <div class="errors">
            <span v-for="error in $store.state.errors" :key="error.id">{{error}}<br></span>
        </div>
        <div class="form" >
            <form action="" id="product_form" @submit.prevent="$store.commit('addProduct')">
                <div>
                    <div class="inp_form">
                        <label for="sku">SKU</label>
                        <input type="text" id="sku"  placeholder="#sku" v-model="$store.state.sku" >
                    </div>
                    <div class="inp_form">
                        <label for="name">Name</label>
                        <input type="text" id="name" placeholder="#name" v-model="$store.state.name" >
                    </div>
                    <div class="inp_form">
                        <label for="price">Price ($)</label>
                        <input type="text" id="price" placeholder="#price" v-model="$store.state.price" >
                    </div>
                </div>


                <div>
                    <select v-model="$store.state.type" name="type" id="productType" @change="$store.commit('getAttributes',$event)" >
                            <option disabled value="0" selected>type</option>
                            <option :key="item.id" v-for="item in $store.state.types" :value="item.id" :id="item.name" >{{item.name}}</option>
                    </select>
                </div>

                <div  class="inp_form" v-for="attribute in $store.state.attributes" :key="attribute.id" :id="attribute.id">
                    <label :for="attribute.name" >{{attribute.name}} ({{attribute.unit}}) </label> 
                    <input :id="attribute.name"  class="input-field" name="field1" type="text" v-model="attribute.value" >
                </div>
                <p>{{$store.state.type.description}}</p>

            </form>
        </div>
    </div>
</template>




<script>

export default {
  name: "AddProduct",
mounted(){
      this.$store.commit('getTypes');
  }
}

</script>


<style scoped>
.container {
    position: relative;
    height: 100%;
    width: 100%;
    overflow: hidden;
  }

header{
  margin-top: 50px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.btns-header {
  margin-right: 50px;
    width: 20%;
    display: flex;
    justify-content: space-around;
}
header h2 {
    margin-left: 20px; 
}
.btn {
  color: #fff;
  border: none;
  background-color: #2c3e50;
  padding: 5px;
  cursor: pointer;
}
.btn a {
    text-decoration: none;
    color: #fff;
}

form {
  width: 200px;
  margin: 50px 20px;
}
form div {
    margin: 20px 0;
}
form input,select {
    margin-bottom: 5px;
    padding: 4px;
    border: 1px solid #2c3e50;
    outline: #2c3e50;
}
::placeholder{
  color: rgb(88, 81, 81);
}
form input {
  margin-left: 20px;
  position: absolute;
  left: 20%;
}

.errors {
    position:absolute;
    margin: 25px 500px;
    color: red;
} 
.inp_form {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
}




</style>