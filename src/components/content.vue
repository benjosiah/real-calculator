<template>
    <div class="all">
        <div class="wrap">
            <div class="display">
               <h2> {{display}}</h2>
                <div v-show="show"> {{cal}}</div>
            </div>
            <div class="keys">
                <input type="button" v-for="key in keys" v-bind:value="key" v-on:click.prevent="dig(key)"> 
            </div>
            <div class="fun">
                <button v-on:click="clear" > <h3> Clear </h3></button>
                <button v-on:click="del" > <h3> Del </h3></button>
                 <button v-for="fun in funs" v-on:click.prevent="gi(fun)"> <h3> {{fun}} </h3></button>
                 
            </div>
        </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      keys: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0, '.', '='],
      funs: ['-', '/', '*', '+'],
      value: '',
      pop:0,
      cal:0,
      display:'0',
      sign:'',
      show:true

    };
  },
  methods: {
       dig: function (id) {
        if(this.display.length<21){
            if (id=='=') {
                this.display=this.cal
                this.value=''
                this.show=false
            }
            else if (this.sign=='') {
                this.value=this.value+id;
                this.display=this.value
                this.cal=parseFloat(this.value);
                this.show=true
            } 
            else if (this.sign=='-'){
                this.value=this.value+id;
                this.cal=this.pop-parseFloat(this.value)  
                this.display=this.display+id
                this.show=true
            } 
            else if (this.sign=='+'){
                this.value=this.value+id;
                this.cal=this.pop+parseFloat(this.value) 
                this.display=this.display+id 
                this.show=true
            
            }
            else if (this.sign=='/'){
                this.value=this.value+id;
                this.cal=this.pop/parseFloat(this.value)
                this.display=this.display+id 
                this.show=true 
            }
            else if (this.sign=='*'){
                this.value=this.value+id;
                this.cal=this.pop*parseFloat(this.value)  
                this.display=this.display+id
                this.show=true
            
            }
        }
         
      },
      gi: function (id){
            if(this.display.length<21){
              this.pop=this.cal
                this.value='';
                this.sign=id;
                this.display=this.display+this.sign
            }  
      },
      clear:function(){
           this.pop=0;
          this.sign='';
          this.value='';
          this.cal=0
          this.display='0'
      },
      del:function(){
          this.display.pop
      }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .all{
        width: 50%;
        min-width: 346px;
        margin: auto;
        height: 500px;
        margin-top: 50px;
        background-color: rgb(58, 44, 77);
         position: relative;
    }
    .wrap{
        width: 100%;
        margin-top: 30px;
        position: absolute;
        top: 30px;

    }
    .display{
        width: 90%;
        margin: auto;
        height: 100px;
        background-color: rgb(223, 154, 154);
        top: 20px;
        right: 36.795px;
        left: 36.795px;
        font-size: 30px;
        text-align: right;
    }
    .display div{
        color: green;
        margin-right: 10px;
        

    }
    .display h2{
        margin: 0px;
        margin-right: 10px;
    }
    .keys{
        width: 65%;
        margin-top:20px ;
        margin-left: 5%;
        float: left;
    }
    .fun{
        width: 25%;
        margin-top: 20px;
        margin-right: 2%;
        float: right;
    }

    .keys input{
        width: 33%;
        height: 70px;
        padding: 4px;
    }
    .fun button{
        width: 80%;
        height:46px;
    }
</style>

