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
  <h2 v-bind:class="isPromoted && 'promoted'">Promoted Movie</h2>
  <!--v-bind classes conditionally -->
  <h2 v-bind:class="isSoldout ? 'soldout' : 'new'">Soldout? Movie</h2>
  <!-- isSoldout: true: class solout; false: class new -->
  <h2 v-bind:class="['new', 'promoted']">Newly promoted movie</h2>
  <!--Array classes binding -->
  <h2 v-bind:class="[isPromoted && 'promoted', isSoldout ? 'soldout' : 'new']">
    Array conditional movie
  </h2>
  <!--Array classes conditional binding -->
  <h2
    v-bind:class="{
      promoted: isPromoted,
      new: !isSoldout,
      soldout: isSoldout,
    }"
  >
    Object conditional movie
  </h2>
  <!--Object classes conditional binding, same Array classes conditional binding -->

  <!-- Binding style -->

  <!-- Binding style array approach, ideal for single inline style property -->
  <h2
    v-bind:style="{
      color: highlightColor,
      'font-size': headerSize + 'px',
      padding: '20px',
    }"
  >
    Inline Style
  </h2>
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

  <h2 v-if="num === 0">The number is zero</h2>
  <h2 v-else-if="num < 0">The number is negative</h2>
  <!--'javascript expression' -->
  <h2 v-else-if="num > 0">The number is positive</h2>
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



  <h1 class="underline soldout">List Rendering </h1>
 
<h2>v-for: iterating over an array of strings, iterating over an array of objects, iterating over an array of arrays, iterating over an object
  </h2>
  <h2>using v-for in template</h2>
  <!-- List Rendering

  using v-for directive -->

  <!--iterating over an array of strings  -->

  <!-- <h2 v-for="name in names" :key="name">{{ name }}</h2> -->
  <h2 v-for="(name, index) in names" :key="name">{{ index }} {{ name }}</h2>
  <!-- value of v-bind key attributes must be unique  -->

  <!--iterating over an array of objects  -->
  <h2 v-for="name in fullNames" :key="name.first">
    {{ name.first }} {{ name.last }}
  </h2>

  <!--iterating over an array of arrays  -->
  <div v-for="actor in actors" :key="actor.name">
    <h2>{{ actor.name }}</h2>
    <h3 v-for="movie in actor.movies" :key="movie">{{ movie }}</h3>
  </div>

  <!--iterating over an object  -->
  <h2 v-for="(value, key, index) in myInfo" :key="value">
    {{ index }} {{ key }} {{ value }}
  </h2>

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


  <h1 class="underline soldout"> Conditional List Rendering </h1>
  <!-- Conditional List Rendering -->
  <template v-for="name in names" :key="name">
    <h2 v-if="name === 'Quynh'">{{ name }}</h2>
  </template>
  <!-- When v-if and v-for are both used on the same element, v-if will be evaluated first. -->


  <h1 class="underline soldout"> Methods in Vue </h1>
  <!-- Methods in Vue  -->
  <h2>{{ 1 + 2 + 3 }}</h2>
  <h2>{{ 12 + 2 + 3 }}</h2>

  <h2>Add method: {{ add(1, 2, 3) }}</h2>
  <h2>Add method: {{ add(12, 2, 3) }}</h2>

  <h2>Multiply method: {{ multiply(2) }}</h2>
  <h2>Multiply method: {{ multiply(baseValue) }}</h2>


  <h1 class="underline soldout">Event Handling   </h1>
  <!-- Event Handling -->
<h2>v-on, multiple events handling</h2>
  <h2>{{ name }}</h2>
  <div>
    <!-- <button v-on:mouseover="name ='Quang'"> Change name</button> -->
    <!-- <button v-on:click="name ='Quang'"> Change name</button> -->
    <button v-on:click="changeName">Change name</button>
    <button v-on:click="changeName($event)">Change name</button>
  </div>

  <h2>{{ count }}</h2>
  <div>
    <button v-on:click="count += 1">Increment</button>
    <button v-on:click="count -= 1">Decrement</button>
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
  <button v-on:click="changeName($event), increment(1, $event)">
    Change name
  </button>


  <h1 class="underline soldout">Form Handling   </h1>
  <!-- Form Handling -->
  <h2> 
  Capture user inputs, 
Inputs,
Textasreas, 
Single select dropdown control, 
Multi select control, 
Checkbox, 
Checkbox group, 
Radio, 
Submit form data </h2>

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

  <!-- Capture user inputs  -->
  <div>
    <!--stringify Presentation -->
    <pre
      >{{ JSON.stringify(formValue, null, 2) }}
</pre
    >
    <!-- The <pre> tag is an HTML tag used to indicate preformatted text. This means that the text within the <pre> tag will be displayed exactly as written, 
with all white spaces preserved, including line breaks, tabs, and multiple spaces. -->

    <!-- Inputs -->
  </div>
  <form @submit.prevent="submitForm">
    <div>
      <label for="name">NAME</label>
      <input type="text" id="name" v-model.trim.lazy="formValue.name" />
    </div>

    <!-- Textasreas -->
    <div>
      <label for="profile">Profile Summary </label>
      <textarea id="profile" v-model="formValue.profileSumary" />
    </div>

    <!-- Single select dropdown control -->
    <div>
      <label for="country">Country</label>
      <select id="country" v-model="formValue.country">
        <option value="">Select a country</option>
        <option value="germany">Germany</option>
        <option value="vietnam">Vietnam</option>
        <option value="china">China</option>
      </select>
    </div>

    <!-- Multi select control -->
    <div>
      <label for="job-location">Job Location</label>
      <select id="job-location" multiple v-model="formValue.jobLocation">
        <option value="germany">Germany</option>
        <option value="vietnam">Vietnam</option>
        <option value="china">China</option>
      </select>
    </div>

    <!-- Single Checkbox  -->
    <div>
      <input
        type="checkbox"
        id="remoteWork"
        v-model="formValue.remoteWork"
        true-value="yes"
        false-value="no"
      />
      <label for="remoteWork">Open to remote work?</label>
    </div>
    <!--  Checkbox group/ Multiple checkboxes -->
    <div>
      <label>Skill set</label>
      <input
        type="checkbox"
        id="html"
        value="html"
        v-model="formValue.skillSet"
      />
      <label for="html">HTML</label>
      <input
        type="checkbox"
        id="css"
        value="css"
        v-model="formValue.skillSet"
      />
      <label for="css">CSS</label>
      <input
        type="checkbox"
        id="javascript"
        value="javascript"
        v-model="formValue.skillSet"
      />
      <label for="javascript">JavaScript</label>
    </div>
    <!-- Radio Group Controll-->
    <div>
      <label>Years of Experience</label>
      <input
        type="radio"
        id="0-2"
        value="0-2"
        v-model="formValue.yearsOfExperience"
      />
      <label for="0-2">0-2</label>
      <input
        type="radio"
        id="3-5"
        value="3-5"
        v-model="formValue.yearsOfExperience"
      />
      <label for="3-5">3-5</label>
      <input
        type="radio"
        id="6-10"
        value="6-10"
        v-model="formValue.yearsOfExperience"
      />
      <label for="6-10">5-10</label>
      <input
        type="radio"
        id="10+"
        value="10+"
        v-model="formValue.yearsOfExperience"
      />
      <label for="10+">10+</label>
      <div>
        <label for="age">Age</label>
        <input
          @keyup.enter="submitForm"
          type="number"
          id="age"
          v-model.number="formValue.age"
        />
      </div>
    </div>
    <!-- Submit form data -->
    <!-- <div>
      <button>Submit</button>
    </div> -->


    <h1 class="underline soldout">Modifiers  </h1>
    <!-- Modifiers 
.trim
If you want whitespace from user input to be trimmed automatically, 
you can add the trim modifier to your v-model-managed inputs:
<input v-model.trim="msg" />

.number
If you want user input to be automatically typecast as a number,
you can add the number modifier to your v-model managed inputs:
<input v-model.number="age" />
If the value cannot be parsed with parseFloat(), then the original value is used instead.
The number modifier is applied automatically if the input has type="number".

.lazy
By default, v-model syncs the input with the data after each input event 
(with the exception of IME composition as stated above). 
You can add the lazy modifier to instead sync after change events:
(synced after "change" instead of "input")
<input v-model.lazy="msg" />
The lazy Modifier is used when syncing is not required instantaneously. 
After each input event is fired from the input element, the v-model modifies the variable. Instead, the lazy modifier updates the value on submit. 
This syncs the value after the change.
The lazy modifier is useful for textarea and input text elements as the elements are changed instantaneously. 
We can change the value once the change is being made. This is pretty useful where the search is being with the help of API. We can prevent unwanted API calls when the user enters the query.
 
 Prevent modifier
 It is a very common need to call event.preventDefault() or event.stopPropagation() inside event handlers. 
 Although we can do this easily inside methods, it would be better if the methods can be purely 
 about data logic rather than having to deal with DOM event details.
 To address this problem, Vue provides event modifiers for v-on.

 the click event's propagation will be stopped
<a @click.stop="doThis"></a>

the submit event will no longer reload the page
<form @submit.prevent="onSubmit"></form>

modifiers can be chained
<a @click.stop.prevent="doThat"></a>

just the modifier
<form @submit.prevent></form>

only trigger handler if event.target is the element itself -->
    <!-- i.e. not from a child element
<div @click.self="doThat">...</div>


Key Modifiers: adding key modifiers for v-on or @ when listening for key events

ex: submit when click enter
1. commenting out submit form:
2. add event binding on html: <input @keyup.enter="submit" />
 only call `submit` when the `key` is `Enter` 

  -->

  <h1 class="underline soldout">Bonus Directives  </h1>
    <!-- Bonus Directives  -->
    <!-- v-once
Render the element and component once only, and skip future updates.
Does not expect expression
Details
On subsequent re-renders, the element/component and all its 
children will be treated as static content and skipped. This can be used to optimize update performance -->
    <h2 v-once>{{ name }}</h2>
    <div>
      <button v-on:click="changeName($event)">Change name</button>
    </div>
    <!-- data: name:"Quynh", name.value does not change to "Quang" when click Change name button.  -->

    <!-- v-pre
Skip compilation for this element and all its children.
Does not expect expression
Details
Inside the element with v-pre, all Vue template syntax will be preserved and rendered as-is.
The most common use case of this is displaying raw mustache tags. -->
    <h2 v-pre>{{ name }}</h2>
  </form>

  <!-- Display data in the UI:
- static html 
- text interpolation 
- simple expressions
- Methods
- Computed Properties -->

<h1 class="underline soldout">Computed Properties </h1>
  <!-- Computed Properties 
Properties that can be bound to the template like data properties.
They are used for composing new data from existing sources.
They are highly performant as they are cached calculations which only update when their dependencies change.-->
  <h2>Fullname - {{ firstName }} {{ lastName }}</h2>
  <h2>Computed Fullname - {{ fullName }}</h2>

  <div>
<pre
      >{{ JSON.stringify(items, null, 2) }}
</pre>
</div>
  <h2>
    Total - {{ items.reduce((total, curr) => (total = total + curr.price), 0) }}
  </h2>
  <!-- This is a template expression in Vue.js that calculates the total of prices of items in an array called items.
items.reduce is an Array method that iterates over the array, applying a callback function to each element, 
and reducing the array to a single value. The first argument of reduce is the callback function that takes two parameters: 
total and curr. The total parameter is the accumulator that is updated with the result of each iteration and is initialized
with the second argument of reduce, which is 0 in this case. The curr parameter is the current element of the array being 
processed.
In this template expression, the callback function adds the price property of the current element (curr) to the accumulator 
(total). So, for each iteration, the total value is updated with the sum of the previous total and the price of the current 
element. The final value of total will be the sum of all price values in the items array.
The result of this expression will be a dynamic value that updates whenever the items array changes. 
The value of {{ items.reduce((total, curr) => (total = total + curr.price), 0) }} will be inserted 
into the HTML template wherever it is used. -->
<button @click="items.push({ id: 4, title: 'Keyboard', price: 50 })">
    Add item
  </button>
<h2>Computed Total - {{ total }}</h2>



<!-- Computed Properties vs Methods -->
<h1 class="underline soldout">Computed Properties vs Methods</h1>
<h2>Method Total- {{ getTotal() }}</h2>
<p>Computed properties and methods in Vue.js are both used to perform dynamic data transformations, but they have some differences in their behavior and usage: <br>

- Computed properties are cached based on their dependencies, which means that they are only re-evaluated when their dependencies change.
 This makes them more efficient for frequently used data transformations, since the result is cached and only recalculated when necessary. 
 Methods, on the other hand, are recalculated every time they are called, regardless of whether their dependencies have changed. <br>

- Computed properties are typically used to transform or derive data from other data properties in the component,
 while methods are used to perform more complex logic or data transformations that cannot be easily expressed as a simple computed property.<br>

- Computed properties are defined as functions that return a value, while methods are defined as functions 
that can have side effects and do not need to return a value.<br>

In general, computed properties should be used when you need to transform or derive data from other data properties in your component, while methods should be used when you need to perform more complex logic or data transformations that cannot be easily expressed as a simple computed property. Additionally, computed properties are more efficient for frequently used data transformations, since their result is cached based on their dependencies.
</p>

</template>

<script>
import _ from "lodash";
export default {
  name: "App",
  data() {
    return {
      greet: "Hello",
      name: "Quynh",
      channel: "<b>Code</b>",
      hack: `<a href="#" onclick="alert('You have been hacked!')">Win a prize!</a>`,
      headingId: "heading",
      isDisabled: true,
      status: "danger",
      isPromoted: true,
      isSoldout: true,
      highlightColor: "orange",
      headerSize: "50",
      headerStyleObject: {
        color: "orange",
        fontSize: "50px",
        padding: "20px",
      },
      baseStyleObject: {
        fontSize: "50px",
        padding: "10px",
      },
      successStyleObject: {
        color: "green",
        backgroungColor: "lightgreen",
        border: "1px solid green",
        padding: "0px",
      },
      dangerStyleObject: {
        color: "darkred",
        backgroundColor: "red",
        border: "1px solid darkred",
      },
      num: "a",
      display: true,
      showElement: false,
      names: ["Quynh", "Quang", "Nam"],
      fullNames: [
        { first: "Quang", last: "Pham" },
        { first: "Quynh", last: "Ngo" },
        { first: "Nam", last: "Nguyen" },
      ],
      actors: [
        {
          name: "Christian Bale",
          movies: ["Batman", "American Psycho"],
        },
        {
          name: "Di Caprio",
          movies: ["Titanic", "Inception"],
        },
      ],
      myInfo: {
        name: "Vishwas",
        channel: "Codevolution",
        course: "Vue 3",
      },
      baseMultiplier: 5,
      baseValue: 2,
      count: 0,
      formValue: {
        name: "",
        profileSumary: "",
        country: "",
        jobLocation: [],
        // remoteWork: false,
        remoteWork: "no",
        skillSet: [],
        yearsOfExperience: "",
        age: null,
      },
      firstName: "Quynh",
      lastName: "Ngo",
      items: [
        {
          id: 1,
          title: "TV",
          price: 100,
        },
        {
          id: 2,
          title: "Phone",
          price: 200,
        },
        {
          id: 3,
          title: "Laptop",
          price: 300,
        },
      ],
    };
  },
  methods: {
    shuffle() {
      console.log(this.names);
      this.names = _.shuffle(this.names);
    },
    changeName(event) {
      this.name = "Quang";
      console.log("Event", event);
    },
    add(a, b, c) {
      return a + b + c;
    },
    multiply(num) {
      return num * this.baseMultiplier;
    },
    increment(num, event) {
      this.count += num;
      console.log("Event", event);
    },
    decrement(num) {
      return (this.count -= num);
    },
    // submitForm(event) {
    // event.preventDefault();
    submitForm() {
      console.log("Form values", this.formValue);
    },
    getTotal(){
      return this.items.reduce((total, curr) => (total = total + curr.price), 0);
    },
  },
  computed: {
    fullName() {
      return `${this.firstName} ${this.lastName}`;
    },
    total(){
      return this.items.reduce((total, curr) => (total = total + curr.price), 0);

    },
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
div {
  display: block;
}
.underline {
  text-decoration: underline;
}
.promoted {
  font-style: italic;
}
.new {
  color: green;
}
.soldout {
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
input[type="text"],
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
