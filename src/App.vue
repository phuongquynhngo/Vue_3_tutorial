<template>
  <!-- Binding Text -->
   <div>{{ greet }} {{ name }}</div> 

  <!-- Binding html -->
  <div v-html="channel"></div>
  <div v-html="hack"></div>

  <!-- Binding to attributes -->
  <h2 v-bind:id="headingId">Heading</h2>
  <button v-bind:disable="isDisabled">Bind</button>

  <!-- Binding classes -->
  <h2 class="underline">Underlined Text</h2>
  <h2 class="underline" v-bind:class="status">Status</h2>
  <h2 v-bind:class="isPromoted && 'promoted'">Promoted Movie</h2> <!--v-bind classes conditionally -->
  <h2 v-bind:class="isSoldout ? 'soldout' : 'new'">Soldout? Movie</h2><!-- isSoldout: true: class solout; false: class new -->
  <h2 v-bind:class="['new', 'promoted']">Newly promoted movie</h2><!--Array classes binding -->
  <h2 v-bind:class="[isPromoted && 'promoted',isSoldout ? 'soldout' : 'new']">Array conditional movie</h2><!--Array classes conditional binding -->
  <h2 v-bind:class="{
    promoted: isPromoted,
    new: !isSoldout,
    soldout: isSoldout,
  }">Object conditional movie</h2><!--Object classes conditional binding, same Array classes conditional binding -->


<!-- Binding style -->

  <!-- Binding style array approach, ideal for single inline style property -->
  <h2 v-bind:style="{
    color: highlightColor,
    'font-size':headerSize +'px',
    padding: '20px'
  }">Inline Style</h2> 
  <!--
  'font-size' in quote, because it is not a single word
  'font-size':headerSize +'px'
  OR: 
  fontSize:headerSize +'px' 
  -->

  <!-- Binding style object approach, ideal for single inline style properties-->
  <h2 v-bind:style="headerStyleObject">Style Object</h2>

  <div v-bind:style="[baseStyleObject, successStyleObject]">Success Style</div> 
  <!-- The last style object gets priority when there are conflicting styles -->

  <div v-bind:style="[baseStyleObject, dangerStyleObject]">Danger Style</div> 


<!--
  v-bind Shorthand
 : instead of v-bind: 

 <h2 :class="isPromoted && 'promoted'">Promoted Movie</h2>
 <h2 v-bind:class="isPromoted && 'promoted'">Promoted Movie</h2>
 
  -->


<!-- Conditional Rendering 
  v-if, v-else, v-else-if: mount and unmount elements to the dom 
  v-show: toggles the display css property
  -->

  <h2 v-if="num===0">The number is zero</h2>
  <h2 v-else-if="num <0">The number is negative</h2>   <!--'javascript expression' -->
  <h2 v-else-if="num >0">The number is positive</h2>
  <h2 v-else>Not a number</h2> 
  <!-- v-else or v-else-if directive must follow the v-if or v-else-if element,
   otherwise this will not work/ not be recognized -->

  <!-- Conditional Rendering  multiple elements -->
  <!-- <div v-if="display">
  <h2>Quynh Ngo</h2>
  <h2>Code</h2>
  <h2>Vue</h2>
  </div> -->
  <template v-if="display">
  <h2>Quynh Ngo</h2>
  <h2>Code</h2>
  <h2>Vue</h2>
  </template> 
  <!-- template tag: invisible wrapper
   to toggle more than one element
   The final rendered result will not include the <template> element.
   -->
  

  <!-- v-show  -->
  <h2 v-show="showElement">Using v-show</h2>
  <h2 v-if="showElement">Using v-if</h2>
  <!-- When showElement property is false: conditional Element using v-if directive is not present in the dom,
  but v-show still present with the display css property set to none
  v-if conditionally renders elements, higher toggle costs, v-if allows us to use other logic blocks in combination with it: v-else and v-else-ifblocks to really build advanced logic
  v-show conditionally displayselements, higher initial render costs, to toggle something frequently
  -->


<!-- List Rendering

  using v-for directive -->

  <!--iterating over an array of strings  -->

  <!-- <h2 v-for="name in names" :key="name">{{ name }}</h2> -->
  <h2 v-for="(name, index) in names" :key="name">{{index}} {{ name }}</h2>
  <!-- value of v-bind key attributes must be unique  -->

  <!--iterating over an array of objects  -->
  <h2 v-for="name in fullNames" :key="name.first">{{ name.first }} {{ name.last }}</h2>

  <!--iterating over an array of arrays  -->
  <div v-for="actor in actors" :key="actor.name">
  <h2 >{{ actor.name }}</h2>
  <h3 v-for="movie in actor.movies" :key="movie">{{ movie }}</h3>
  </div>

  <!--iterating over an object  -->
  <h2 v-for="(value,key,index) in myInfo" :key="value">{{index}} {{key}} {{ value }}</h2>
   
   <!-- using v-for in template -->
  <template v-for="name in names" :key="name">
  <h2>{{ name }}</h2>
  <hr />
  </template>
  
 <!-- List and keys 
 key here is a special attribute being bound with v-bind. 
 It should not be confused with the property key variable when using v-for with an object.
 To give Vue a hint so that it can track each node's identity, 
 and thus reuse and reorder existing elements, you need to provide a unique key attribute for each item.
 The key binding expects primitive values - i.e. strings and numbers
 -->
 <template v-for="name in names" :key="name">
    <h2>{{ name }}</h2>
    <input placeholder="Last name" />
    <hr />
  </template>
  <button @click="shuffle">Shuffle!</button>



<!-- Conditional List Rendering -->
  <template v-for="name in names" :key="name">
  <h2 v-if="name ==='Quynh'">{{ name }}</h2>
  </template>
<!-- When v-if and v-for are both used on the same element, v-if will be evaluated first. -->




<!-- Methods in Vue  -->
<h2>{{ 1+2+3 }}</h2>
<h2>{{ 12+2+3 }}</h2>

<h2>Add method: {{ add(1,2,3) }}</h2>
<h2>Add method: {{ add(12,2,3) }}</h2>

<h2>Multiply method: {{ multiply(2) }}</h2>
<h2>Multiply method: {{ multiply(baseValue) }}</h2>


<!-- Event Handling -->

<h2>{{ name }}</h2>
<div>
  <!-- <button v-on:mouseover="name ='Quang'"> Change name</button> -->
<!-- <button v-on:click="name ='Quang'"> Change name</button> -->
<button v-on:click="changeName"> Change name</button>
<button v-on:click="changeName($event)"> Change name</button>

</div>

<h2>{{ count }}</h2>
<div>
<button v-on:click="count +=1">Increment</button>
<button v-on:click="count -=1">Decrement</button>
</div>
<div>
<button v-on:click="increment(1)">Increment 1</button>
<button v-on:click="increment(2)">Increment 2</button>
<button v-on:click="decrement(1)">Decrement 1</button>
<button v-on:click="decrement(2)">Decrement 2</button>
</div>

<!-- v-on Shorthand
 @ instead of v-on:
 -->
 <div>
<button @click="increment(1, $event)">Increment 1</button>
<button @click="increment(2)">Increment 2</button>
<button @click="decrement(1)">Decrement 1</button>
<button @click="decrement(2)">Decrement 2</button>
</div>

<!-- multiple events handling -->
<button v-on:click="changeName($event), increment(1, $event)"> Change name</button>


<!-- Form Handling -->

<!-- Capture user inputs, 
Inputs,
Textasreas, 
Single select dropdown control, 
Multi select control, 
Checkbox, 
Checkbox group, 
Radio, 
Submit form data -->

<!-- v-model  directive : 2 way binding refers binding from tho template to data and from data back to template, 
ensures model and view are always in sync -->

 <div> <!--stringify Presentation -->
<pre>
{{ JSON.stringify(formValue, null , 2) }}
</pre>
<!-- The <pre> tag is an HTML tag used to indicate preformatted text. This means that the text within the <pre> tag will be displayed exactly as written, 
with all white spaces preserved, including line breaks, tabs, and multiple spaces. -->
</div>
 <form>
 <div>
 <label for="name">NAME</label>
 <input type="text" id="name" v-model="formValue.name">
 </div>

 <div>
 <label  for="profile">Profile Summary </label>
 <textarea  id="profile" v-model="formValue.profileSumary" />
 </div>

 <div>
<label for="country">Country</label>
<select id="country" v-model="formValue.country">
<option value="">Select a country</option>
<option value="germany">Germany</option>
<option value="vietnam">Vietnam</option>
<option value="china">China</option>
</select>
</div>

<div>
<label for="job-location">Job Location</label>
<select id="job-location" multiple v-model="formValue.jobLocation">

<option value="germany">Germany</option>
<option value="vietnam">Vietnam</option>
<option value="china">China</option>
</select>
</div>
 </form>




</template>

<script>
import _ from "lodash";
export default {
  name: 'App',
  data(){
    return{
      greet:'Hello',
      name:"Quynh",
      channel:'<b>Code</b>',
      hack: `<a href="#" onclick="alert('You have been hacked!')">Win a prize!</a>`,
      headingId: 'heading',
      isDisabled: true,
      status: 'danger',
      isPromoted: true,
      isSoldout: true,
      highlightColor: 'orange',
      headerSize: '50',
      headerStyleObject:{
        color: 'orange',
        fontSize: '50px',
        padding: '20px',},
      baseStyleObject:{
        fontSize: '50px',
        padding: '10px',
      },
      successStyleObject:{
        color: 'green',
        backgroungColor:'lightgreen',
        border:  '1px solid green',
        padding: '0px'
    
      },
      dangerStyleObject:{
        color: 'darkred',
        backgroundColor: 'red',
        border: '1px solid darkred',              
      },
      num:"a",
      display: true,
      showElement: false,
      names: ["Quynh", "Quang", "Nam"],
      fullNames: [
        {first: 'Quang', last:'Pham'},
        {first: 'Quynh', last:'Ngo'},
        {first: 'Nam', last:'Nguyen'},
      ],
      actors: [
        {
          name: 'Christian Bale',
          movies: ['Batman', 'American Psycho'],
        },
        {
          name: 'Di Caprio',
          movies: ['Titanic', 'Inception'],
        },
      ],
      myInfo: {
        name: 'Vishwas',
        channel: 'Codevolution',
        course: 'Vue 3',
      },
      baseMultiplier:5,
      baseValue:2,
      count:0,
      formValue:{
        name:'',
        profileSumary:'',
        country:'',
        jobLocation:[],
      },
    };
   
  },
  methods: {
    shuffle() {
      console.log(this.names);
      this.names = _.shuffle(this.names);
    },
    changeName(event){
      this.name ='Quang'
      console.log('Event', event)
    },
    add(a,b,c){
      return a+b+c
    },
    multiply(num){
      return num * this.baseMultiplier
    },
    increment(num,event){
       this.count +=num
       console.log('Event', event)
    },
    decrement(num){
      return this.count -=num
    }
  },

};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
div{
  display: block;
}
.underline{
  text-decoration: underline;
}
.promoted{
  font-style: italic;
}
.new{
  color: green;
}
.soldout{
  color: red;
}
label {
  font-weight: bold;
  display: flex;
  margin-bottom: 5px;
}
input + label {
  font-weight: bold;
  display: inline-flex;
  margin-right: 20px;
}
input[type='text'],
textarea,
select {
  display: block;
  width: 400px;
  padding: 6px 12px;
  font-size: 14px;
  line-height: 1.42857143;
  color: #555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
