  # Object-Oriented JavaScript
  <br/>

  ## 1. Objects in Depth
  <hr />
  <br/>

  ### 1.1 Introduction
  <hr />
  <br/>

  #### Arrays
  <hr />
  At its core, an array is just an ordered collection of elements, enclosed by square brackets (i.e., [ and ]). Here s a variable called myArray, which is assigned to an empty array:<br/><br/>

  ```const myArray = [];```
  <br/><br/>

  Each element in an array is referenced by a numeric key called an index, which starts from zero and increments by one for each additional element in the array. Check out the following example:

  <code>const fruits = ['apple', 'banana', 'orange', 'grape', 'lychee'];<br/>
  console.log(fruits);<br/>
  // ['apple', 'banana', 'orange', 'grape', 'lychee'];</code>
  <br/><br/>

  If we want to retrieve the first (left-most) element in fruits, we access that element by its index:

  <code>fruits[0];
  // 'apple'</code>
  <br/><br/>

  Likewise, this is how we can access the last (right-most) element in fruits:

  <code>fruits[4];
  // 'lychee'</code>
  <br/><br/>

#### Objects
 <hr />
  Fundamentally, an object is a collection of associated key/value pairs. We create an object with curly brackets (i.e., { and }). Here s a variable called myObject, which is assigned to an empty object:

  ```const myObject = {};```
  <br/><br/>

  While elements in arrays are referenced by a numeric index, keys in an object must be named explicitly, like color or year. Check out the following example:

  <code>const car = {<br/>
    color: 'red',<br/>
    year: 1992,<br/>
    isPreOwned: true<br/>
  };</code>
  <br/><br/>

  Let's break this down and see what s going on:
  - The variable that is assigned to the object is named car.
  - Curly brackets are used to define the car object.
  - Individual keys (e,g, color) are associated with a single value ('red' in this case). 
  - These key/value pairs are connected by a colon (:).
  - Each distinct key/value pair, known as a property of that object, is separated from other properties by a comma (,).
  - The car object therefore contains three properties.

  Unlike arrays, objects are unordered collections. For example, the car object above could be written with the key/value pairs in a different order, and it wouldn't change how you d access car s items:

  <code>const car = {<br/>
    isPreOwned: true,<br/>
    color: 'red',<br/>
    year: 1992<br/>
  };</code>
  <br/><br/>

  #### Object property syntax
  <hr />
  Another thing to note is that keys (i.e., the names of the object s properties) are strings, but quotation marks surrounding these strings are optional as long as the string is also a valid Javascript identifier (i.e., you could use it as a variable name or function name). 
  As a result, the following three objects are equivalent:

  <code>const course = { courseId: 711 };   // ← no quotes around the courseId key<br/>
  const course = { 'courseId': 711 };       // ← single quotes around the courseId key<br/>
  const course = { "courseId": 711 };       // ← double quotes around the courseId key</code>
  <br/><br/>

  You'll commonly find quotation marks omitted from property names. Certain situations require them to be included, especially if the property name:
  - Is a reserved word (e.g., for, if, let, true, etc.).
  - Contains spaces or special characters that cannot appear in a variable name (i.e., punctuation other than $, and _ -- most accented characters).

  For the exact rules for property names, feel free to check out the links at the end of this section.<br/><br/>

  #### JavaScript Objects Might Look Familiar
  <hr/>
  If you ve had past experience with Python or Ruby, objects are quite similar to dictionaries and hashes (respectively). Though they may look the same, there are key differences to be mindful of.

  First, Ruby hashes and JavaScript objects have similar functionality: they are both collections of values accessible by keys. However, values are accessed in Ruby hashes a bit differently. Consider the following Ruby hash:

  <code>book = {<br/>
    title: 'To Kill a Mockingbird',<br/>
    author: 'Harper Lee',<br/>
    published: 1960<br/>
  }</code>

  Because the hash keys are symbols (rather than strings), properties are accessed _by_ that symbol:

  <code>book[:title]<br/>
  #'To Kill a Mockingbird'</code>

  Any attempts to using JavaScript s dot notation or square bracket notation lead to undesirable results:

  <code>book.title<br/>
  #undefined method `title' for #<Hash> (NoMethodError)</code>

  <code>book['title']<br/>
  #nil</code>

  Another major difference between Ruby hashes and JavaScript objects are that objects can take a function as a property value (we ll take a deep dive into this in the next section). This functionality does not exist for Ruby hashes!

  On the other hand, Python dictionaries have some similar functionality to objects in JavaScript as well, with some notable differences. For one, keys in Python dictionaries must be something hashable (e.g., a string, a number, a float, etc.). The following is a valid object in JavaScript:

  ```const javascriptObject = { name: 'George Orwell', year: 1984 }```

  However, it would be invalid as a Python dictionary:
  <code>python_dictionary = {name: 'George Orwell', year: 1984}<br/>
  #Traceback (most recent call last):
  #NameError: name 'name' is not defined</code>

  A quick fix would be to convert the Python dictionary s keys into strings:
  ```my_dictionary = {'name': 'George Orwell', 'year': 1984}```

  Above all else, you can also leverage objects in JavaScript not just to hold data, but for many powerful functionalities such as constructors. This is an object-oriented JavaScript course, so we ll take a deep dive into these features throughout this course!

  | Arrays | Objects |
  |---|---|
  | [] | {} |
  | Ordered | Unordered | 
  | Indexed | Key-value pairs | 
  <br/>

  #### Accessing object properties
  <hr/>
  So now that we know what objects look like, how do we retrieve information from them? In other words: how do we access their values? There are two ways: dot notation and square bracket notation. Consider this bicycle object:

  <code>const bicycle = {<br/>
    color: 'blue',<br/>
    type: 'mountain bike',<br/>
    wheels: {<br/>
      diameter: 18,<br/>
      width: 8<br/>
    }<br/>
  };</code>

  Using dot notation, we can access bicycle s color property by writing:
  <code>bicycle.color;<br/>
  // 'blue'</code>

  Similarly, we can access the same property using square bracket notation by writing:
  <code>bicycle['color'];<br/>
  // 'blue'</code>

  Both expressions are equivalent, and will each return 'blue'.

  What about nested objects? To retrieve the value of the width property of the object contained within bicycle s wheels property, you can do the following with dot notation:
  <code>bicycle.wheels.width;<br/>
  // 8</code>

  And with square bracket notation:
  <code>bicycle['wheels']['width'];<br/>
  // 8</code>

  Again, both expressions are equivalent, and will each return 8.
  <br/><br/>

  #### Dot notation limitation
  <hr/>
  Note that while dot notation may be easier to read and write, it can t be used in every situation. For example, let s say there s a key in the above bicycle object that is a number. An expression like bicycle.1 will cause a error, while bicycle[1] returns the intended value:

  <code>bicycle.1;<br/>
  // Uncaught SyntaxError: Unexpected number</code>

  <code>bicycle[1];<br/>
  // (returns the value of the `1` property)</code>

  Another issue is when variables are assigned to property names. Let s say we declare myVariable, and assign it to the string 'color':

  ```const myVariable = 'color';```

  ```bicycle[myVariable]``` returns 'blue' because the variable myVariable gets substituted with its 
  value (the string 'color') and ```bicycle['color']```'s value is 'blue'. However, ```bicycle.myVariable; ```
  returns undefined:

  <code>bicycle[myVariable];<br/>
  // 'blue'</code>

  <code>bicycle.myVariable;<br/>
  // undefined</code>

  It may seem odd, but recall that all property keys in a JavaScript object are strings, even if the quotation marks are omitted. With dot notation, the JavaScript interpreter looks for a key within bicycle whose value is 'myVariable'. Since there isn t such a key defined in the object, the expression returns undefined.
  <br/><br/>

  #### Summary
  <hr/>
  In JavaScript, an object is an unordered collection of properties. Each property consists of a 
  key/value pair, and can reference either a primitive (e.g., strings, numbers, booleans, etc.) 
  or another object. Unlike elements in an array, which are accessed by a numeric index, properties 
  in objects are accessed by their key name using either square bracket notation or dot notation. 
  For a closer look at object fundamentals, check out Intro to JavaScript linked below.

  Now that we know how to read existing properties in an object, how do we go about creating new 
  properties? What about modifying existing properties, or even adding and removing properties 
  altogether? We ll answer all this and more in the very next section!
  <br/><br/>

  #### Further Research
  <hr/>

  - Intro to JavaScript: https://www.udacity.com/course/intro-to-javascript--ud803
  - Unquoted property names / object keys in JavaScript: https://mathiasbynens.be/notes/javascript-properties
  - Valid JavaScript variable names in ECMAScript 5: https://mathiasbynens.be/notes/javascript-identifiers
  - Valid JavaScript variable names in ECMAScript 6: https://mathiasbynens.be/notes/javascript-identifiers-es6
  <br/><br/>

  ### 1.2. Create and modify properties
  <hr/>
  <br/>

  #### Creating Objects
  <hr/>
  To create a new, blank (i.e., “empty”) object, you can use object literal notation, or the Object() constructor function. If you re not familiar with constructor functions, no need to worry! We'll jump into them in-depth in Lesson 3. For now, just know that the following two expressions are 
  equivalent:<br/><br/>

  Using literal notation:<br/>
  ```const myObject = {};```
  <br/><br/>

  Using the Object() constructor function:<br/>
  ```const myObject = new Object();```
  <br/><br/>

  While both methods ultimately return an object without properties of its own, the Object() constructor function is a bit slower and more verbose. As such, the recommended way to create new objects in JavaScript is to use literal notation.

  **The recommended way to create objects in JS is literal notation.**
  <br/><br/>

  #### Modifying Properties
  <hr/>
  Keep in mind that data within objects are mutable, meaning that data can be changed. There are 
  a few exceptions to this, but for now, let s see how we can modify/reassign existing properties 
  in an object.<br/><br/>

  Consider the following cat object:

  <code>const cat = {<br/>
    age: 2,<br/>
    name: 'Bailey',<br/>
    meow: function () {<br/>
      console.log('Meow!');<br/>
    },<br/>
    greet: function (name) {<br/>
      console.log(`Hello ${name}`);<br/>
    }<br/>
  };</code>
  <br/><br/>

  Now, let s go ahead change it up a bit!

  <code>cat.age += 1;<br/>
  cat.age;<br/>
  // 3</code>

  <code>cat.name = 'Bambi';<br/>
  cat.name;<br/>
  // 'Bambi'</code>
  <br/><br/>

  After incrementing the value of the age property by 1, and reassigning name s value to 'Bambi', our cat object now looks like:

  <code>{<br/>
    age: 3,<br/>
    name: 'Bambi',<br/>
    meow: function () {<br/>
      console.log('Meow!');<br/>
    },<br/>
    greet: function (name) {<br/>
      console.log(`Hello ${name}`);<br/>
    }<br/>
  };</code>
  <br/><br/>

  #### Adding Properties
  <hr/>
  Properties can be added to objects simply by specifying the property name, then giving it a value. Let s start off with a blank object, then add two properties:

  <code>const printer = {};<br/>
  printer.on = true;<br/>
  printer.mode = 'black and white';</code>

  The above example uses dot notation to add properties, but keep in mind that square bracket notation works just as well:

  ```printer['remainingSheets'] = 168;```

  Likewise, we can add a method to the printer object in a similar manner. This time, the value of the property is an anonymous (i.e., unnamed) function:

  <code>printer.print = function () {<br/>
    console.log('The printer is printing!');<br/>
  };</code>

  Great! The complete printer object now looks like the following:

  <code>{<br/>
    on: true,<br/>
    mode: 'black and white',<br/>
    remainingSheets: 168,<br/>
    print: function () {<br/>
      console.log('The printer is printing!');<br/>
    }<br/>
  }</code>
  <br/><br/>

  #### Removing Properties
  <hr/>
  Recall that since objects are mutable, not only can we modify existing properties (or even add new ones) -- we can also delete properties from objects.<br/><br/>

  Say that the printer object above actually doesn t have any modes (i.e., 'black and white', 'color', etc.). We can go ahead and remove that property from printer using the delete operator.

  <code>delete printer.mode;<br/>
  // true</code>

  Note that delete directly mutates the object at hand. If we try to access a deleted property, the JavaScript interpreter will no longer be able to find the mode property because the mode key (along with its value, true) have been deleted:

  <code>printer.mode;<br/>
  // undefined</code>

  Great! Let s see this all in action below.

  - Al borrar una propiedad con delete, return true cuando borra exitosamente.
  - Si intentamos acceder a una propiedad borrada retornará undefined.
  - Salvo pocas excepciones, las propiedades de los objetos son mutables.
  - Se puede agregar propiedades a los objetos con dot ay bracket notation.

  #### Exercises
  <hr/>  
  Write an expression to delete the numWindows property from house.

  <code>let house = {<br/>
    color: 'green',<br/>
    numRooms: 4,<br/>
    numWindows: 8,<br/>
    forSale: false<br/>
  };<br/><br/>

  delete house.numWindows<br/><br/>

  let house = {<br/>
    color: 'green',<br/>
    numRooms: 4,<br/>
    forSale: false<br/>
  };</code>

  Write an expression to add a new hasGarage property to house. 
  Set the value of the hasGarage property to true.

  ```house.hasGarage = true;```

  #### Passing Arguments
  <hr/>

  #### Passing a Primitive
  <hr/>
  In JavaScript, a primitive (e.g., a string, number, boolean, etc.) is immutable. In other words, any changes made to an argument inside a function effectively creates a copy local to that function, and does not affect the primitive outside 
  of that function. Check out the following example: <br/><br/>

  <code>function changeToEight(n) {<br/>
    n = 8; // whatever n was, it is now 8... but only in this function!<br/>
  };<br/>
  let n = 7;<br/>
  changeToEight(n);<br/>
  console.log(n); // 7</code>

  ```changeToEight()``` takes in a single argument, n, and changes it to 8. However, this 
  change only exists inside the function itself. We then pass the global variable n 
  (which is assigned the value 7) into the function. After invoking it, n is still 
  equal to 7.

  Atention: 

  <code>let n = { number: 7 };<br/>
  function changeToEight(n) {<br/>
    n = {<br/>
      numero: 8<br/>
    };<br/>
  };<br/>
  changeToEight(n);<br/>
  console.log(n); // { number: 7 }</code>

  Now:

  <code>var n = { number: 7 };<br/>
  function changeToEight(n) {<br/>
      n.numero = 8<br/>
  };<br/>
  changeToEight(n);<br/>
  console.log(n);  // { number: 7, numero: 8 }</code>

  #### Passing an Object
  <hr/>
  On the other hand, objects in JavaScript are mutable. If you pass an object into a function, Javascript passes a reference to that object. Let s see what happens if we pass an object into a function and then modify a property:

  <code>let originalObject = {<br/>
    favoriteColor: 'red'<br/>
  };<br/><br/>

  function setToBlue(object) {<br/>
    object.favoriteColor = 'blue';<br/>
  }<br/><br/>

  setToBlue(originalObject);<br/><br/>

  originalObject.favoriteColor;<br/>
  // 'blue'</code>

  In the above example, originalObject contains a single property, favoriteColor, which has a value of 'red'. We pass originalObject into the setToBlue() function and invoke it. After accessing originalObject s favoriteColor property, we see that the value is now 'blue'!<br/>

  How did this happen? Well, since objects in JavaScript are passed by reference, if we make changes to that reference, we re actually directly modifying the original object itself!<br/>

  What's more: the same rule applies when re-assigning an object to a new variable, and then changing that copy. Again, since objects are passed by reference, the original object is changed as well. Let's take a look at this more closely with another example.<br/>

  **When we modify primitives, a local copy is created in the function scope, but globally it still has the same value and that is not possible for us to access the assigned value in the scope.
  JS objects are passed by reference, if we make changes to that reference, we are directly modifying the object itself.
  The same thing happens when we reassign an object to a new variable and then modify that copy.
  Since objects are passed by reference, the original object is also modified, mutates.**

  Consider this iceCreamOriginal object, which shows the amount of ice cream cones each 
  instructor has eaten:

  <code>const iceCreamOriginal = {<br/>
    Andrew: 3,<br/>
    Richard: 15<br/>
  };</code>

  Let's go ahead and make assign a new variable to iceCreamOriginal. We ll then check the value of its Richard property:

  <code>const iceCreamCopy = iceCreamOriginal;<br/>
  iceCreamCopy.Richard;<br/>
  // 15</code>

  As expected, the expression iceCreamCopy.Richard; returns 15 (i.e., it is the same value as the Richard property in iceCreamOriginal). Now, let s change the value in the copy, then check the results:

  <code>iceCreamCopy.Richard = 99;<br/>
  iceCreamCopy.Richard;<br/>
  // 99<br/><br/>

  iceCreamOriginal.Richard;<br/>
  // 99</code>

  Since objects are passed by reference, making changes to the copy (iceCreamCopy) has a direct effect on the original object (iceCreamOriginal) as well. In both objects, the value of the Richard property is now 99.
  <br/><br/>

  #### Comparing an Object with Another Object
  <hr/>
  On the topic of references, let s see what happens when we compare one object with another object. The following objects, parrot and pigeon, have the same methods and properties:

  <code>const parrot = {<br/>
    group: 'bird',<br/>
    feathers: true,<br/>
    chirp: function () {<br/>
      console.log('Chirp chirp!');<br/>
    }<br/>
  };<br/><br/>

  const pigeon = {<br/>
    group: 'bird',<br/>
    feathers: true,<br/>
    chirp: function () {<br/>
      console.log('Chirp chirp!');<br/>
    }<br/>
  };</code>

  Naturally, one might expect the parrot object and pigeon object to be equal. After all, both objects look exactly the same! Let s compare parrot and pigeon to find out:

  <code>parrot === pigeon;<br/>
  // false</code>

  What's going on here? As it turns out, the expression will only return true when comparing two references to exactly the same object. Using what we now know about passing objects, let's confirm this. To start off, let s create a new variable, myBird, and assign it to one of the objects above:

  ```const myBird = parrot;```

  As we ve just learned, myBird not only refers to the same object as parrot -- they are the same object! If we make any updates to myBird s properties, parrot s properties will be 
  updated with exactly the same changes as well. Now, the comparison will return true:

  <code>myBird === parrot;<br/>
  // true</code>

  So since pigeon is not the same object as myBird or parrot, any comparisons between myBird 
  and pigeon will return false:

  <code>myBird === pigeon;<br/>
  // false</code>
  <br/><br/>

  Inmutables:
  - 8
  - 'How are you today?'
  - 3.14
  - true
  <br/><br/>

  Mutables:
  - { numProperties: 1 }
  - [0, 1, 2, 3, 4, 5]
  - function() { console.log() }
  <br/><br/>

  Consider the following:

  <code>let string = 'orange';<br/>
  function changeToApple(string) {<br/>
    string = 'apple';<br/>
  }<br/>

  changeToApple(string);<br/>

  console.log(string);<br/>

  // Orange</code>
  <br/><br/>

  Now:

  <code>let string = 'orange';<br/>

  function changeToApple(string) {<br/>
    string2 = 'apple';<br/>
    return string;<br/>
  }<br/>

  changeToApple(string);<br/>

  console.log(string2);<br/>
  // apple</code>
  <br/><br/>

  Consider the following object, oven:

  <code>const oven = {<br/>
    type: 'clay',<br/>
    temperature: 400<br/>
  };</code>

  What is the value of oven's temperature property after the following operations?

  <code>const newOven = oven;<br/>
  newOven.temperature += 50; <br/>
  // 450</code>
  <br/><br/>

  #### Summary
  <hr/>
  Objects are commonly created with literal notation, and can include properties that point to functions called methods. Methods are accessed the same way as other properties of objects, and can be invoked the same way as regular functions, except they automatically have access to the other properties of their parent object.<br/>

  By default, objects are mutable (with a few exceptions), so data within them can be altered. <br/>

  New properties can be added, and existing properties can be modified by simply specifying the property name and assigning (or re-assigning) a value. Additionally, properties and methods of an object can be deleted as well with the delete operator, which directly mutates the object.<br/>

  We ve modified objects quite a bit in this section, and even added new methods into them. In the very next section, we ll take a closer look at invoking these methods, as well as how these methods can directly access and modify an object itself!
  <br/><br/>

  #### Further Research
  <hr/>

  - The 'delete' operator on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete
  <br/><br/>

  ### 1.3. Functions vs. Methods
  <hr/>
  At this point, we ve mostly seen objects with properties that behave more like attributes. 
  That is, properties such as color or type are data that describe an object, but they don't "do" anything. We can extend functionality to objects by adding methods to them.<br/>

  Say that we have a function, sayHello(), which simply logs a message to the console:

  <code>function sayHello () {<br/>
    console.log('Hi there!');<br/>
  }</code>
  <br/><br/>

  Now, say that we also have a developer object with a single property, name:

  <code>const developer = {<br/>
    name: 'Andrew'<br/>
  };</code>
  <br/><br/>

  If we want to add the sayHello() function into the developer object, we can add the same way as we add other new properties: by providing property name, then giving it a value. This time, the value of the property is a function!<br/>

  <code>developer.sayHello = function () {<br/>
    console.log('Hi there!');<br/>
  };</code>
  <br/><br/>

  This is how the updated developer object looks:

  <code>{<br/>
    name: 'Andrew',<br/>
    sayHello: function () {<br/>
      console.log('Hi there!');<br/>
    }<br/>
  }</code>
  <br/><br/>

  So now that a sayHello property has been defined, how do we go about calling (i.e., invoking) its referenced function?
  <br/><br/>

  #### Calling Methods
  <hr/>
  We can access a function in an object using the property name. Again, another name for a function property of an object is a method. We can access it the same way that 
  we do with other properties: by using dot notation or square bracket notation. Let's take a look back at the updated developer object above, then invoke its sayHello() method:

  <code>const developer = {<br/>
    name: 'Andrew',<br/>
    sayHello: function () {<br/>
      console.log('Hi there!');<br/>
    }<br/>
  };<br/><br/>

  developer.sayHello();<br/>
  // 'Hi there!'<br/><br/>

  developer['sayHello']();<br/>
  // 'Hi there!'</code>

  Just like calling a function, an object s method is called by adding parentheses at the end of the method s name. Note that both dot notation and square bracket notation return the same result!
  <br/><br/>

  #### Passing Arguments Into Methods
  <hr/>
  If the method takes arguments, you can proceed the same way, too:

  <code>const developer = {<br/>
    name: 'Andrew',<br/>
    sayHello: function () {<br/>
      console.log('Hi there!');<br/>
    },<br/>
    favoriteLanguage: function (language) {<br/>
      console.log(`My favorite programming language is ${language}`);<br/>
    }<br/>
  };<br/><br/>

  developer.favoriteLanguage('JavaScript');<br/>
  // My favorite programming language is JavaScript</code>
  <br/><br/>

  - Los métodos como las funciones, para invocarlas es necesario incluir () al final
  - Los métodos como las funciones, toman argumentos.
  - Un método es una propiedad que apunta a una función.
  <br/><br/>

  Write an expression that invokes the alerter() function in the following array, myArray:

  <code>const myArray = [ function alerter() { alert('Hello!'); } ];<br/>
  myArray[0]();</code>
  <br/><br/>

  Write an expression that invokes the function referenced by the bell object s ring property:

  <code>const bell = {<br/>
    color: 'gold',<br/>
    ring: function () {<br/>
      console.log('Ring ring ring!');<br/>
    }<br/>
  };<br/><br/>

  bell.ring();</code>


  #### Call Methods by Property Name
  <hr/>
  We ve been using anonymous functions (i.e., functions without a name) for object methods. However, naming those functions is still valid JavaScript syntax. Consider the following object, greeter:

  <code>const greeter = {<br/>
    greet: function sayHello() {<br/>
      console.log('Hello!');<br/>
    }<br/>
  };</code>

  Note that the greet property points to a function with a name: sayHello. Whether this function is named or not, greet is invoked the same way:

  <code>greeter.greet();<br/>
  // 'Hello!'</code>

  Named functions are great for a smoother debugging experience, since those functions will have a useful name to display in stack traces. They re completely optional, however, and you ll often read code written by developers who prefer one way or the other.
  <br/><br/>

  #### A Method Can Access the Object it was Called On
  <hr/>
  Recall that an object can contain data and the means to manipulate that data. But just how can an object reference its own properties, much less manipulate some of those properties itself? This is all possible with the this keyword!

  Using this, methods can directly access the object that it is called on. Consider the following object, triangle:

  <code>const triangle = {<br/>
    type: 'scalene',<br/>
    identify: function () {<br/>
      console.log(`This is a ${this.type} triangle.`);<br/>
    }<br/>
  };</code>
  <br/><br/>

  Note that inside the identify() method, the value this is used. When you say this, what you re really saying is "this object" or "the object at hand." this is what gives the identify() method direct access to the triangle object s properties:

  <code>triangle.identify();<br/>
  // 'This is a scalene triangle.'</code>

  When the identify() method is called, the value of this is set to the object it was called on: triangle. As a result, the identify() method can access and use triangle s type property, as seen in the above console.log() expression.

  Note that this is a reserved word in JavaScript, and cannot be used as an identifier (e.g. variable names, function names, etc.).

  - _this_ refers to the containing object
  - Using _this_, methods can access and manipulate the properties of the object.
  - The value of _this_ is set when the method is called on an object and that value refers to the object.
  - _this_ is a reserved keyword.

  Let's make sure we re still on the same page! Write an expression that invokes the function referenced by the tree object s growOneFoot property:

  <code>const tree = {<br/>
    type: 'redwood',<br/>
    leaves: 'green',<br/>
    height: 80,<br/>
    age: 15,<br/>
    growOneFoot: function () {<br/>
      this.height += 1;<br/>
    }<br/>
  };<br/><br/>

  tree.growOneFoot();</code>

  #### Exercises
  <hr/>
  Create an object called 'chameleon' with two properties:<br/>
  1. 'color', whose value is initially set to 'green' or 'pink'<br/>
  2. 'changeColor', a function which changes 'chameleon''s 'color' to 'pink'<br/>
  if it is 'green', or to 'green' if it is 'pink'.<br/><br/>

  <code>const chameleon = {<br/>
    color: 'pink',<br/>
    changeColor: function () {<br/>
        if(this.color == 'pink') {<br/>
            this.color = 'green';<br/>
        } else {<br/>
            this.color = 'pink';<br/>
        }<br/>
    }<br/>
  };<br/>
  chameleon.changeColor();<br/>
  console.log(chameleon.color);</code>
  <br/><br/>

  
  #### The value of this
  <hr/>
  Depending on how a function is called, this can be set to different values! Later in this course, we ll take a deep dive into different ways that functions can be invoked, and how each approach influences the value of this.
  <br/><br/>

  #### Summary
  <hr/>
  A method is a function property of an object. It is accessed the same way as any other property of the object (i.e., using dot notation or square bracket notation), and is invoked the same way as a regular function outside of an object (i.e., adding parentheses to the end of the expression).<br/><br/>

  Since an object is a collection of data and the means to operate on that data, a method can access the object it was called on using the special this keyword. The value of this 
  is determined when a method is invoked, and its value is the object on which the method was called. Since this is a reserved word in JavaScript, its value cannot be used as an 
  identifier. Feel free to check out the links below for an additional look at methods and their relationship with this.<br/><br/>

  We ve spent a bit of time on this inside objects, but did you know that the value of this can have different meanings outside an object? In the next section, we ll take a close look at globals, their relationship with this, and the implications of using them.
  <br/><br/>

  #### Further Research
  <hr/>

  - Defining Methods on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Defining_methods

  - 'this' in Methods: https://javascript.info/object-methods#this-in-methods
  <br/><br/>

  ### 1.4. Beware of Globals
  <hr/>
  <br/>

  #### Things that Belong to Objects
  <hr/>

  Previously, we saw that the properties and methods contained inside an object belong to that object. Let s drive this home with one quick example:

  <code>const chameleon = {<br/>
    eyes: 2,<br/>
    lookAround: function () {<br/>
      console.log(`I see you with my ${this.eyes} eyes!`);<br/>
    }<br/>
  };<br/><br/>

  chameleon.lookAround();<br/>
  // 'I see you with my 2 eyes!'</code>

  We ve already looked at how this inside a method refers to the object that the method was called on. Let s take a closer look at chameleon s lookAround() method.

  <code>lookAround: function () {<br/>
    console.log(`I see you with my ${this.eyes} eyes!`);<br/>
  }</code>

  Inside the function body is the code this.eyes. Since the lookAround() method was called on the chameleon object as chameleon.lookAround();, the value of this is the chameleon 
  object itself! As such, this.eyes is the number 2, since it refers to the value of the chameleon object s eyes property.

  Now, let s check out a different example. What do you think will be the value of this inside the following code?

  <code>function whoThis () {<br/>
    this.trickyish = true<br/>
  }<br/>
  whoThis();</code>

  #### Write your thoughts below.
  <hr/>

  What do you think will be the value of this inside the following code? Window object<br/>
  What does the above expression output? Undefined
  <br/><br/>

  #### this and Function Invocation
  <hr/>
  Let s compare the code from the chameleon object with the whoThis() code.

  <code>const chameleon = {<br/>
    eyes: 2,<br/>
    lookAround: function () {<br/>
      console.log(`I see you with my ${this.eyes} eyes!`);<br/>
    }<br/>
  };<br/>
  chameleon.lookAround();<br/><br/>

  function whoThis () {<br/>
    this.trickyish = true<br/>
  }<br/>
  whoThis();</code>
  <br/><br/>

  #### this in the Function/Method
  <hr/>

  Before we dive into how this all works, take a look at the use of this inside 
  both of these code snippets:

  // from the chameleon code:<br/>
  ```console.log(`I see you with my ${this.eyes} eyes!`);```

  // from the whoThis() code:<br/>
  ```this.trickyish = true```

  There is some other code around them, but both of them have the format _this.<some-identifier<some-identifier>>_. For our purposes of discovering the value of this, it does not
  matter that in the chameleon code, we re using this to retrieve a property, while in the whoThis() code, we re using this to set a property.

  So, in both of these cases, the use of this is virtually identical.
  <br/><br/>

  #### Compare the Structures of the Function/Method
  <hr/>
  Now, I want you to pay attention to the differences in structure of how the two snippets of code are invoked. The lookAround() code is a method because it belongs to an object. Since it s a method, it s invoked as a property on the chameleon object:

  ```chameleon.lookAround();```

  Now compare that with the whoThis() code. whoThis() is not a method; it's a plain, old, 
  regular function. And look at how the whoThis() function is invoked:

  ```whoThis();```

  Just like every normal function is invoked; it's just the name of the function and the parentheses (there s no object and no dot in front of it).
  <br/><br/>

  #### this and Invocation
  <hr/>
  How the function is invoked determines the value of this inside the function. ← That 
  sentence is really important, so read that two more times...we ll wait!<br/><br/>

  Because .lookAround() is invoked as a method, the value of this inside of .lookAround() is whatever is left of the dot at invocation. Since the invocation looks like:

  ```chameleon.lookAround();```

  The chameleon object is left of the dot. Therefore, inside the .lookAround() method, this will refer to the chameleon object!

  Now let s compare that with the whoThis() function. Since it is called as a regular function (i.e., not called as an method on an object), its invocation looks like:

  ```whoThis();```

  Well, there is no dot. And there is no object left of the dot. So what is the value 
  of this inside the whoThis() function? This is an interesting part of the JavaScript 
  language.

  When a regular function is invoked, the value of this is the global window object.

  Let's see it all in action!
  <br/><br/>

  #### The window Object
  <hr/>

  If you haven't worked with the window object yet, this object is provided by the browser environment and is globally accessible to your JavaScript code using the identifier, window. 
  This object is not part of the JavaScript specification (i.e., ECMAScript); instead, it is developed by the W3C.

  This window object has access to a ton of information about the page itself, including:

  - The page s URL (window.location;)
  - The vertical scroll position of the page (window.scrollY)
  - Scrolling to a new location (window.scroll(0, window.scrollY + 200); to scroll 200 
  pixels down from the current location)
  - Opening a new web page (window.open("https://www.udacity.com/");)

  <code>const car = {<br/>
    numberOfDoors: 4,<br/>
    drive: function () {<br/>
      console.log(`Get in one of the ${this.numberOfDoors} doors, and let s go!`);<br/>
    }<br/>
  };<br/>
  const letsRoll = car.drive;<br/>
  letsRoll();</code>

  What does you think this refers to in the code above? The window object
  <br/><br/>

  #### Global Variables are Properties on window
  <hr/>

  Since the window object is at the highest (i.e., global) level, an interesting thing happens with global variable declarations. Every variable declaration that is made at 
  the global level (outside of a function) automatically becomes a property on the window object!<br/>

  Here we can see that the currentlyEating variable is set to 'ice cream'. Then, we immediately see that the window now has a currentlyEating property! Checking this property against the currentlyEating variable shows us that they are identical.

  <code>var currentlyEating = 'ice cream';<br/>
  window.currentlyEating === currentlyEating<br/>
  // true</code>
  <br/><br/>

  #### Globals and var, let, and const
  <hr/>
  The keywords var, let, and const are used to declare variables in JavaScript. var has been around since the beginning of the language, while let and const are significantly newer additions (added in ES6).

  Only declaring variables with the var keyword will add them to the window object. If you declare a variable outside of a function with either let or const, it will not be added as 
  a property to the window object.

  <code>let currentlyEating = 'ice cream';<br/>
  window.currentlyEating === currentlyEating<br/>
  // false!</code>
  <br/><br/>

  #### Global Functions are Methods on window
  <hr/>
  Similarly to how global variables are accessible as properties on the window object, any global function declarations are accessible on the window object as methods:

  <code>function learnSomethingNew() {<br/>
    window.open('https://www.udacity.com/');<br/>
  }<br/><br/>

  window.learnSomethingNew === learnSomethingNew<br/>
  // true</code>

  Declaring the learnSomethingNew() function as a global function declaration (i.e., it s globally accessible and not written inside another function) makes it accessible to your code as either learnSomethingNew() or window.learnSomethingNew().

  Which of the following variables and functions will be available on the window object?

  <code>var iceCreamEaten = 1;<br/><br/>

  function consume (numberOfGallons) {<br/>
    var result = iceCreamEaten + numberOfGallons;<br/>
    function updateTotals (newTotal) {<br/>
      iceCreamEaten = result;<br/>
    }<br/>
    updateTotals();<br/>
  }<br/>
  consume(3);</code>
  <br/><br/>

  #### Avoid Globals
  <hr/>
  We ve seen that declaring global variables and functions add them as properties to the window object. Globally-accessible code sounds like something that might be super helpful, right? I mean, wouldn t it be great if you could always be within arms reach of some ice cream (or is that just my lifelong dream)?<br/><br/>

  Counterintuitively, though, global variables and functions are not ideal. There are actually a number of reasons why, but the two we ll look at are:
  - Tight coupling
  - Name collisions
  <br/><br/>

  #### Tight Coupling
  <hr/>
  Tight coupling is a phrase that developers use to indicate code that is too dependent on the details of each other. The word "coupling" means the "pairing of two items together.
  " In tight coupling, pieces of code are joined together in a way where changing one unintentionally alters the functioning of some other code:

  <code>var instructor = 'Richard';<br/>
  function richardSaysHi() {<br/>
    console.log(`${instructor} says 'hi!'`);<br/>
  }</code>

  In the code above, note that the instructor variable is declared globally. 
  The richardSaysHi() function does not have a local variable that it uses to store the instructor's name. Instead, it reaches out to the global variable and uses that. 
  If we refactored this code by changing the variable from instructor to teacher, this would break the richardSaysHi() function (or we d have to update it there, too!). 
  This is a (simple) example of tightly-coupled code.
  <br/><br/>

  #### Name Collisions
  <hr/>
  A name collision occurs when two (or more) functions depend on a variable with the same name. A major problem with this is that both functions will try to update the variable and or set the variable, but these changes are overridden by each other!

  Let s look at an example of name collision with this DOM manipulation code:

  <code>let counter = 1;<br/>
  function addDivToHeader () {<br/>
    const newDiv = document.createElement('div');<br/>
    newDiv.textContent = 'div number ' + counter;<br/><br/>

    counter = counter + 1;<br/><br/>

    const headerSection = document.querySelector('header');<br/>
    headerSection.appendChild(newDiv)<br/>
  }<br/><br/>

  function addDivToFooter() {<br/>
    const newDiv = document.createElement('div');<br/>
    newDiv.textContent = 'div number ' + counter;<br/><br/>

    counter = counter + 1;<br/><br/>

    const headerSection = document.querySelector('footer');<br/>
    headerSection.appendChild(newDiv)<br/>
  }</code>

  In this code, we have an addDivToHeader() function and a addDivToFooter() function. 
  Both of these functions create a \<div> element and increment a counter variable.

  This code looks fine, but if you try running this code and adding a few \<div>'s to the \<header> and \<footer> elements, you ll find that the numbering will get off! Both 
  addDivToHeader() and addDivToFooter() expect a global counter variable to be accessible to them -- not change out from under them!

  Since both functions increment the counter variable, if the code alternates between calling addDivToHeader() and addDivToFooter(), then their respective \<div>'s will not 
  have numerically ascending numbers. For example, if we had the following calls:

  <code>addDivToHeader();<br/>
  addDivToHeader();<br/>
  addDivToFooter();<br/>
  addDivToHeader();</code>

  The developer probably wanted the \<header> to have three \<div> elements with the numbers 1, 2, and 3 and the \<footer> element to have a single \<div> with the number 1. However,   what this code will produce is a \<header> element with three \<div> but with the numbers 1, 2, and 4 (not 3) and a \<footer> element with the number 3...these are very different results. But it s happening because both functions depend on the counter variable and both update it.<br/>

  So what should you do instead? You should write as few global variables as possible. 
  Write your variables inside of the functions that need them, keeping them as close to where they are needed as possible. Now, there are times when you ll need to write global variables, but you should only write them as a last resort.
  <br/><br/>

  ### Summary
  <hr/>
  The window object is provided by the browser and is not part of the JavaScript language or specification. Any global variable declarations (i.e., those that use var) or global 
  function declarations are added as properties to this window object. Excessive use of global variables is not a good practice, and can cause unexpected problems to accurately-written code.

  Whether you re working with the window object, or with an object you create yourself, recall that all objects are made up of key/value pairs. In the next section, we'll check 
  out how to extract these individual keys or values!
  <br/><br/>

  #### Further Research
  <hr/>

  - The window object on MDN: https://developer.mozilla.org/en-US/docs/Web/API/Window
  - The window specification on W3C: https://www.w3.org/TR/html5/browsers.html#the-window-object
  - Globals are Bad: http://wiki.c2.com/?GlobalVariablesAreBad
  - Coupling on Wikipedia: https://bit.ly/2m07ZOj
  - Name Collision on Wikipedia: https://en.wikipedia.org/wiki/Name_collision
  <br/><br/>

  ### 1.5. Extracting Properties and Values
  <hr/>
  <br/>

  #### Object Methods
  <hr/>
  Do you remember earlier when we used the Object() constructor function to create (i.e., instantiate) new objects with the new keyword?

  ```const myNewFancyObject = new Object();```

  The Object() function actually includes a few methods of its own to aid in the development of your applications. These methods are:

  <code>Object.keys()<br/>
  Object.values()</code>

  Whether you re building logic in your code, or just writing a utility "helper" function, feel free to use these methods as necessary. Let s see how each of these work!

  <code>let array = ['a', 'b', 'c', 'd', 'e'];<br/>
  console.log(Object.keys(array), Object.values(array));<br/>
  // [ '0', '1', '2', '3', '4' ] [ 'a', 'b', 'c', 'd', 'e' ]<br/><br/>

  let object = {<br/>
    key1: 'value1',<br/>
    key2: 'value2',<br/>
    key3: 'value3',<br/>
    key4: 'value4'<br/>
  };<br/><br/>

  console.log(Object.keys(object), Object.values(object));<br/>
  // [ 'key1', 'key2', 'key3', 'key4' ] [ 'value1', 'value2', 'value3', 'value4' ]<br/><br/>

  let object2 = {<br/>
    key1: {<br/>
        subkey1: 'subvalue1',<br/>
        subkey2: 'subvalue2'<br/>
    },<br/>
    key2: 'value2',<br/>
    key3: 'value3',<br/>
    key4: 'value4'<br/>
  };<br/><br/>

  console.log(Object.keys(object2), Object.values(object2));<br/>
  // [ 'key1', 'key2', 'key3', 'key4' ] [{ subkey1: 'subvalue1', subkey2: 'subvalue2' }, 'value2', 'value3', 'value4']
  </code>
  <br/><br/>

  #### Object.keys() and Object.values()
  <hr/>

  At its core, an object is just a collection of key/value pairs. What if we want to extract only the keys from an object? Say we have this object representing a real-life dictionary:

  <code>const dictionary = {<br/>
    car: 'automobile',<br/>
    apple: 'healthy snack',<br/>
    cat: 'cute furry animal',<br/>
    dog: 'best friend'<br/>
  };</code>

  Having a collection of just the words (i.e., the dictionary object s keys) may be particularly 
  useful. While we could use a for...in loop to iterate through an object and build our own list 
  of keys, it can get a bit messy and verbose. Thankfully, JavaScript provides an abstraction 
  just for this!

  When Object.keys() is given an object, it extracts just the keys of that object, then returns 
  those keys in an array:

  <code>Object.keys(dictionary);<br/>
  // ['car', 'apple', 'cat', 'dog']</code>

  So Object.keys() gives returns an array of the provided object s property names. Likewise, if we want a list of the values of an object, we can use Object.values():

  <code>Object.values(dictionary);<br/>
  // ['automobile', 'healthy snack', 'cute furry animal', 'best friend']</code>
  <br/><br/>

  #### Support for Object.keys() and Object.values()
  <hr/>

  - Object.keys() has been around for quite a long time, so it is fully supported by every 
  browser.
  - Object.values(), on the other hand, is significantly newer. It was officially added to the language specification in 2017. However, just because it s been added to the specification, it necessarily doesn t mean your browser supports it yet!
  
  How do you know if your browser does support Object.values()? Check out the Browser Compatibility table

  What is true about Object.keys()? Select all that apply.
  Object.keys() will return an array of strings and will return them in the same order as they would be when using a for loop.

  What is true about Object.values()? Select all that apply.
  Object.values() will return the items in the same order as when using a for loop. They won't always be strings, because they can have nested objects.
  <br/><br/>

  #### Summary
  <hr/>
  The Object() constructor function has access to several methods to aid in development. To extract property names and values from an object, we can use:

  - Object.keys() returns an array of a given object s own keys (property names). 
  - Object.values() returns an array of a given object s own values (property values).
  <br/><br/>

  #### Further Research
  <hr/>
  
  - Object.keys() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys

  - Object.values() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values

  - Browser Compatibility: http://tokenposts.blogspot.com.au/2012/04/javascript-objectkeys-browser.html
  <br/><br/>
  
  ### 1.5. Summary
  <hr/>
  <br/>
  
  #### Further Research
  <hr/>
  
  - JavaScript: The Good Parts by Douglas Crockford: http://javascript.crockford.com/
  
  - JavaScript: The Good Parts via Goodreads: https://www.goodreads.com/book/show/2998152-javascript