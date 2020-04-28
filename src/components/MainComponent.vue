<template>
  <div class="hello">
    <h2>Array:{{sArr}}</h2>
    <button v-on:click="onclick('asc')" type="button">order elements by asc</button>
    <button v-on:click="onclick('desc')" type="button">order elements by desc</button>

    <h2>Result:{{rArr}}</h2>
  </div>
</template>

<script>
export default {
  name: 'MainComponent',
  props: {
    msg: String
  },
  data(){
    return{
      arr:[{date: '10.01.2017'}, {date: '05.11.2016'}, {date: '21.13.2002'}],
      sArr:"",
      rArr:""
    }
  },
  methods:{
    compare:function(type){
      return ( a, b )=> {
      let splitFdate = a.date.split(".");
      let fDate = new Date(parseInt(splitFdate[2]), parseInt(splitFdate[1]-1), parseInt(splitFdate[0]), 22, 0, 0).getTime();
      let splitSdate = b.date.split(".");
      let sDate = new Date(parseInt(splitSdate[2]), parseInt(splitSdate[1]-1), parseInt(splitSdate[0]), 22, 0, 0).getTime();
        if ( fDate < sDate ){
          return type=='asc'? -1 : 1;
        }
        if ( fDate > sDate ){
          return type=='asc'? 1 : -1;
        }
        return 0;
      }
    },
    onclick:function(type){
      this.arr.sort(this.compare(type));
      this.rArr = JSON.stringify(this.arr);
    }
  },
  mounted(){
    this.sArr = JSON.stringify(this.arr);
    this.rArr = JSON.stringify([]);
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
</style>
