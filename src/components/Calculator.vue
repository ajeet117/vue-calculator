<template>
<div >
  <c-box w="400px" mx="auto" h="90px" textAlign="right" bg="black" outline="1px" outlineStyle="solid" outlineColor="black" mt="4" py="4">
  <c-text fontSize="xl" m="0" color="white">
  {{prev}}{{operand}}
  </c-text>
  <c-text fontSize="3xl" m="0" color="white">{{current}}</c-text>
  </c-box>
  <c-grid w="400px" template-columns="repeat(4, 1fr)"  mx="auto"  textAlign="center" fontSize="xl">
  <c-box h="20" bg="lightgrey"  @click="addNumber('7')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">7</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('8')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">8</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('9')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">9</c-box>
  <c-box h="20" bg="orange.300" @click="divide"  display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">/</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('4')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">4</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('5')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">5</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('6')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">6</c-box>
  <c-box h="20" bg="orange.300" @click="multiply"  display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">*</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('1')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">1</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('2')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">2</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('3')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">3</c-box>
  <c-box h="20" bg="orange.300" @click="add"  display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">+</c-box>
  <c-box h="20" bg="lightgrey"  @click="dot" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">.</c-box>
  <c-box h="20" bg="lightgrey"  @click="addNumber('0')" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">0</c-box>
  <c-box h="20" bg="lightgrey"  @click="equal" display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">=</c-box>
  <c-box h="20" bg="orange.300" @click="subtract"  display="flex" align-items="center" justify-content="center" outline="1px" outlineStyle="solid" outlineColor="black">-</c-box>
</c-grid>
</div>
</template>

<script>
import { CGrid,CBox,CText  } from "@chakra-ui/vue";
export default {
  name: 'Calculator',
  components:{
    CGrid,
    CBox,
    CText
  },
  data()
  {
    return{
      prev:"",
      current:"",
      operator:"",
      operand:"",
      equalsClicked:false
    }
  },
  methods:{
    addNumber(num)
    {
      if(this.equalsClicked)
      {
        this.current=""
      }
      this.equalsClicked=false
      this.current +=num;
      
    },
    change()
    {
      this.prev=this.current;
      this.current="";
    },
    dot()
    {
      if(this.current.indexOf('.') === -1)
      {
      this.addNumber(".")
      }
    },
    operatorEqual()
    {
      if(this.operand !== "")
      {
        this.prev=this.operator(parseFloat(this.prev),parseFloat(this.current));
        this.current=""
      }
    },
    add()
    {
      this.operatorEqual();
      this.operand="+"
      if(this.prev === "")
      {
      this.change();
      }
      this.operator =(num1,num2) => (num1+num2)
      
      
    },
    divide()
    {
      this.operatorEqual();
      if(this.prev === "")
      {
      this.change();
      }
      this.operand="/"
      this.operator =(num1,num2) => (num1/num2)
      
    },
    multiply()
    {
      this.operatorEqual();
      if(this.prev === "")
      {
      this.change();
      }
      this.operand="*"
      this.operator= (num1,num2) => (num1*num2)
      
    },
    subtract()
    {
      this.operatorEqual();
      if(this.prev === "")
      {
      this.change();
      }
      this.operand="-"
      this.operator= (num1,num2) => (num1-num2)
      
    },
    equal()
    {
      this.current=this.operator(parseFloat(this.prev),parseFloat(this.current));
      this.prev=""
      this.operand=""
      this.equalsClicked=true
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
