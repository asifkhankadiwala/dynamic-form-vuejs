<template>
  <b-container class="mt-5">
      <b-row>
           <b-col lg="9" md="9">
            <b-card
              title="List Items"
              tag="article" 
              class="mb-2">
              <b-card-text> 
                <b-row class="mb-3"  >
                    <b-col lg="3" md="3">
                        Addon
                    </b-col>
                    <b-col lg="2" md="2">
                        Price
                    </b-col>
                    <b-col lg="2" md="2">
                        Quantity
                    </b-col>
                    <b-col lg="2" md="2">
                        Total
                    </b-col>
                </b-row>
                <template   v-for="(data,index) in addons">
                  <b-row class="mb-3" v-bind:key="data.index">
                    <b-col lg="3" md="3">
                       <b-form-select  class="custom-select" v-model="data.addon_id" :options="addons_list"></b-form-select>
                    </b-col>
                    <b-col lg="2" md="2">
                      <b-form-input type="number" v-model="data.price" placeholder="price"  ></b-form-input>
                    </b-col>

                    <b-col lg="2" md="2">
                      <b-form-input type="number" v-model="data.quantity" placeholder="Quantity"></b-form-input>
                    </b-col>
                    <b-col lg="3" md="3">
                      <b-form-input type="number" :value="data.total = data.quantity*data.price" placeholder="Min"></b-form-input>
                    </b-col>

                    <b-col lg="2" md="2">
                       <b-button @click="addRow()"  v-bind:class="{ 'vhidden': index+1!=addons.length   }"    variant="outline-primary" class="mx-2" size="sm"><p class="h5 m-0">  <b-icon icon="plus"></b-icon> </p> </b-button>
                       <b-button  @click="removeRow(index)"  v-bind:class="{ 'vhidden': addons.length==1   }"  variant="outline-danger " class="deletebutton" size="sm"><p class="h6  m-0">  <b-icon icon="trash"></b-icon></p></b-button>
                    </b-col>
                  </b-row>
                </template>
              </b-card-text>
            </b-card>
          </b-col>
          <b-col lg="3" md="3">
             <b-card
              title="data"
              tag="article" 
              class="mb-2 jsoncard">
              <b-card-text> 
              <pre>{{ addons  }}</pre>
            </b-card-text>
          </b-card>
          </b-col>
      </b-row>
  </b-container>
</template>
<script>
export default {
  name: 'HelloWorld',
  data() {
      return {
        addons: [
                  { id: 1, addon_id:'3', price:30, quantity:2, total:60},
                  { id: 2, addon_id:'2', price:20, quantity:5, total:100},
                  { id: 3, addon_id:'4', price:40, quantity:1, total:40},
                  { id: 4, addon_id:'1', price:10, quantity:5, total:50}
                ],
        addons_list: [
          { value: null, text: 'Please select an option'},
          { value: '1', text: 'Addon 1'},
          { value: '2', text: 'Addon 2'},
          { value: '3', text: 'Addon 3'},
          { value: '4', text: 'Addon 4'}
        ]
      }
    },
    methods:{
      addRow(){
        this.addons.push( { id: null,addon_id: null, price:0, quantity:1, total:0 });
      },
      removeRow(i){
        this.addons.splice( i,1)
      },
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.custom-select{
  display: inline-block;
    width: 100%;
    height: calc(1.5em + .75rem + 2px);
    padding: .375rem 1.75rem .375rem .75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #495057;
    vertical-align: middle;
    background: #fff url(data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' width='4' height='5'%3E%3Cpath fill='%23343a40' d='M2 0L0 2h4zm0 5L0 3h4z'/%3E%3C/svg%3E) no-repeat right .75rem center/8px 10px;
    border: 1px solid #ced4da;
    border-radius: .25rem;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
}
.deletebutton {
  padding: 6px 10px;
}
.vhidden {
  visibility: hidden;
}
.jsoncard {
  max-height: 600px;
    overflow: auto;
}
</style>
