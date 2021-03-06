  # Object-Oriented JavaScript

  ## 1. Objects in Depth

  ### 1.1 Introduction

  #### 1.1.1. Arrays
  At its core, an array is just an ordered collection of elements, enclosed by square brackets (i.e., [ and ]). Here s a variable called myArray, which is assigned to an empty array:<br/><br/>

  ```
  const myArray = [];
  ```
  <br/>

  Each element in an array is referenced by a numeric key called an index, which starts from zero and increments by one for each additional element in the array. Check out the following example:

  ```
  const fruits = ['apple', 'banana', 'orange', 'grape', 'lychee'];
  console.log(fruits);
  // ['apple', 'banana', 'orange', 'grape', 'lychee'];
  ```
  <br/>

  If we want to retrieve the first (left-most) element in fruits, we access that element by its index:

  ```
  fruits[0];
  // 'apple'
  ```
  <br/>

  Likewise, this is how we can access the last (right-most) element in fruits:

  ```fruits[4];
  // 'lychee'
  ```
  <br/>

  #### 1.1.2. Objects
  Fundamentally, an object is a collection of associated key/value pairs. We create an object with curly brackets (i.e., { and }). Here s a variable called myObject, which is assigned to an empty object:

  ```
  const myObject = {};
  ```
  <br/>

  While elements in arrays are referenced by a numeric index, keys in an object must be named explicitly, like color or year. Check out the following example:

  ```
  const car = {
    color: 'red',
    year: 1992,
    isPreOwned: true
  };
  ```
  <br/>

  Let's break this down and see what s going on:
  - The variable that is assigned to the object is named car.
  - Curly brackets are used to define the car object.
  - Individual keys (e,g, color) are associated with a single value ('red' in this case). 
  - These key/value pairs are connected by a colon (:).
  - Each distinct key/value pair, known as a property of that object, is separated from other properties by a comma (,).
  - The car object therefore contains three properties.

  Unlike arrays, objects are unordered collections. For example, the car object above could be written with the key/value pairs in a different order, and it wouldn't change how you d access car s items:

  ```
  const car = {
    isPreOwned: true,
    color: 'red',
    year: 1992
  };
  ```
  <br/>

  #### 1.1.3. Object property syntax
  Another thing to note is that keys (i.e., the names of the object s properties) are strings, but quotation marks surrounding these strings are optional as long as the string is also a valid Javascript identifier (i.e., you could use it as a variable name or function name). 
  As a result, the following three objects are equivalent:

  ```
  const course = { courseId: 711 };         // ??? no quotes around the courseId key
  const course = { 'courseId': 711 };       // ??? single quotes around the courseId key
  const course = { "courseId": 711 };       // ??? double quotes around the courseId key
  ```
  <br/>

  You'll commonly find quotation marks omitted from property names. Certain situations require them to be included, especially if the property name:
  - Is a reserved word (e.g., for, if, let, true, etc.).
  - Contains spaces or special characters that cannot appear in a variable name (i.e., punctuation other than $, and _ -- most accented characters).

  For the exact rules for property names, feel free to check out the links at the end of this section.<br/><br/>

  #### 1.1.4. JavaScript Objects Might Look Familiar
  If you ve had past experience with Python or Ruby, objects are quite similar to dictionaries and hashes (respectively). Though they may look the same, there are key differences to be mindful of.

  First, Ruby hashes and JavaScript objects have similar functionality: they are both collections of values accessible by keys. However, values are accessed in Ruby hashes a bit differently. Consider the following Ruby hash:

  ```
  book = {
    title: 'To Kill a Mockingbird',
    author: 'Harper Lee',
    published: 1960
  }
  ```
  <br/>

  Because the hash keys are symbols (rather than strings), properties are accessed _by_ that symbol:

  ```
  book[:title]
  #'To Kill a Mockingbird'
  ```
  <br/>

  Any attempts to using JavaScript s dot notation or square bracket notation lead to undesirable results:

  ```
  book.title
  #undefined method `title' for #<Hash> (NoMethodError)
  
  book['title']
  #nil
  ```
  <br/>

  Another major difference between Ruby hashes and JavaScript objects are that objects can take a function as a property value (we ll take a deep dive into this in the next section). This functionality does not exist for Ruby hashes!

  On the other hand, Python dictionaries have some similar functionality to objects in JavaScript as well, with some notable differences. For one, keys in Python dictionaries must be something hashable (e.g., a string, a number, a float, etc.). The following is a valid object in JavaScript:

  ```
  const javascriptObject = { name: 'George Orwell', year: 1984 }
  ```
  <br/>

  However, it would be invalid as a Python dictionary:
  ```
  python_dictionary = {name: 'George Orwell', year: 1984}
  #Traceback (most recent call last):
  #NameError: name 'name' is not defined
  ```
  <br/>

  A quick fix would be to convert the Python dictionary s keys into strings:
  ```
  my_dictionary = {'name': 'George Orwell', 'year': 1984}
  ```
  <br/>

  Above all else, you can also leverage objects in JavaScript not just to hold data, but for many powerful functionalities such as constructors. This is an object-oriented JavaScript course, so we ll take a deep dive into these features throughout this course!

  | Arrays | Objects |
  |---|---|
  | [] | {} |
  | Ordered | Unordered | 
  | Indexed | Key-value pairs | 
  <br/>

  #### 1.1.5. Accessing object properties
  So now that we know what objects look like, how do we retrieve information from them? In other words: how do we access their values? There are two ways: dot notation and square bracket notation. Consider this bicycle object:

  ```
  const bicycle = {
    color: 'blue',
    type: 'mountain bike',
    wheels: {
      diameter: 18,
      width: 8
    }
  };
  ```
  <br/>

  Using dot notation, we can access bicycle s color property by writing:
  ```
  bicycle.color;
  // 'blue'
  ```
  <br/>

  Similarly, we can access the same property using square bracket notation by writing:
  ```
  bicycle['color'];
  // 'blue'
  ```
  <br/>

  Both expressions are equivalent, and will each return 'blue'.

  What about nested objects? To retrieve the value of the width property of the object contained within bicycle s wheels property, you can do the following with dot notation:
  ```
  bicycle.wheels.width;
  // 8
  ```
  <br/>

  And with square bracket notation:
  ```
  bicycle['wheels']['width'];
  // 8
  ```
  <br/>

  Again, both expressions are equivalent, and will each return 8.
  <br/><br/>

  #### 1.1.6. Dot notation limitation
  Note that while dot notation may be easier to read and write, it can t be used in every situation. For example, let s say there s a key in the above bicycle object that is a number. An expression like bicycle.1 will cause a error, while bicycle[1] returns the intended value:

  ```
  bicycle.1;
  // Uncaught SyntaxError: Unexpected number

  bicycle[1];
  // (returns the value of the `1` property)
  ```
  <br/>

  Another issue is when variables are assigned to property names. Let s say we declare myVariable, and assign it to the string 'color':

  ```
  const myVariable = 'color';
  ```
  <br/>

  ```bicycle[myVariable]``` returns 'blue' because the variable myVariable gets substituted with its 
  value (the string 'color') and ```bicycle['color']```'s value is 'blue'. However, ```bicycle.myVariable;``` returns undefined:

  ```
  bicycle[myVariable];
  // 'blue'
  
  bicycle.myVariable;
  // undefined
  ```
  <br/>

  It may seem odd, but recall that all property keys in a JavaScript object are strings, even if the quotation marks are omitted. With dot notation, the JavaScript interpreter looks for a key within bicycle whose value is 'myVariable'. Since there isn t such a key defined in the object, the expression returns undefined.
  <br/><br/>

  #### 1.1.7. Summary
  In JavaScript, an object is an unordered collection of properties. Each property consists of a 
  key/value pair, and can reference either a primitive (e.g., strings, numbers, booleans, etc.) 
  or another object. Unlike elements in an array, which are accessed by a numeric index, properties 
  in objects are accessed by their key name using either square bracket notation or dot notation. 
  For a closer look at object fundamentals, check out Intro to JavaScript linked below.

  Now that we know how to read existing properties in an object, how do we go about creating new 
  properties? What about modifying existing properties, or even adding and removing properties 
  altogether? We ll answer all this and more in the very next section!
  <br/><br/>

  #### 1.1.8. Further Research
  - Intro to JavaScript: https://www.udacity.com/course/intro-to-javascript--ud803
  - Unquoted property names / object keys in JavaScript: https://mathiasbynens.be/notes/javascript-properties
  - Valid JavaScript variable names in ECMAScript 5: https://mathiasbynens.be/notes/javascript-identifiers
  - Valid JavaScript variable names in ECMAScript 6: https://mathiasbynens.be/notes/javascript-identifiers-es6
  <br/><br/>

  ### 1.2. Create and modify properties

  #### 1.2.1. Creating Objects
  To create a new, blank (i.e., ???empty???) object, you can use object literal notation, or the Object() constructor function. If you re not familiar with constructor functions, no need to worry! We'll jump into them in-depth in Lesson 3. For now, just know that the following two expressions are 
  equivalent:<br/><br/>

  Using literal notation:<br/>
  ```
  const myObject = {};
  ```
  <br/>

  Using the Object() constructor function:<br/>
  ```
  const myObject = new Object();
  ```
  <br/>

  While both methods ultimately return an object without properties of its own, the Object() constructor function is a bit slower and more verbose. As such, the recommended way to create new objects in JavaScript is to use literal notation.

  **The recommended way to create objects in JS is literal notation.**
  <br/><br/>

  #### 1.2.2. Modifying Properties
  Keep in mind that data within objects are mutable, meaning that data can be changed. There are 
  a few exceptions to this, but for now, let s see how we can modify/reassign existing properties 
  in an object.<br/><br/>

  Consider the following cat object:

  ```
  const cat = {
    age: 2,
    name: 'Bailey',
    meow: function () {
      console.log('Meow!');
    },
    greet: function (name) {
      console.log(`Hello ${name}`);
    }
  };
  ```
  <br/>

  Now, let s go ahead change it up a bit!

  ```
  cat.age += 1;
  cat.age;
  // 3

  cat.name = 'Bambi';
  cat.name;
  // 'Bambi'
  ```
  <br/>

  After incrementing the value of the age property by 1, and reassigning name s value to 'Bambi', our cat object now looks like:

  ```
  {
    age: 3,
    name: 'Bambi',
    meow: function () {
      console.log('Meow!');
    },
    greet: function (name) {
      console.log(`Hello ${name}`);
    }
  };
  ```
  <br/>

  #### 1.2.3. Adding Properties
  Properties can be added to objects simply by specifying the property name, then giving it a value. Let s start off with a blank object, then add two properties:

  ```
  const printer = {};
  printer.on = true;
  printer.mode = 'black and white';
  ```
  <br/>

  The above example uses dot notation to add properties, but keep in mind that square bracket notation works just as well:

  ```
  printer['remainingSheets'] = 168;
  ```
  <br/>

  Likewise, we can add a method to the printer object in a similar manner. This time, the value of the property is an anonymous (i.e., unnamed) function:

  ```
  printer.print = function () {
    console.log('The printer is printing!');
  };
  ```
  <br/>

  Great! The complete printer object now looks like the following:

  ```
  {
    on: true,
    mode: 'black and white',
    remainingSheets: 168,
    print: function () {
      console.log('The printer is printing!');
    }
  }
  ```
  <br/>

  #### 1.2.4. Removing Properties
  Recall that since objects are mutable, not only can we modify existing properties (or even add new ones) -- we can also delete properties from objects.<br/><br/>

  Say that the printer object above actually doesn t have any modes (i.e., 'black and white', 'color', etc.). We can go ahead and remove that property from printer using the delete operator.

  ```
  delete printer.mode;
  // true
  ```
  <br/>

  Note that delete directly mutates the object at hand. If we try to access a deleted property, the JavaScript interpreter will no longer be able to find the mode property because the mode key (along with its value, true) have been deleted:

  ```
  printer.mode;
  // undefined
  ```
  <br/>

  Great! Let s see this all in action below.
  - Al borrar una propiedad con delete, return true cuando borra exitosamente.
  - Si intentamos acceder a una propiedad borrada retornar?? undefined.
  - Salvo pocas excepciones, las propiedades de los objetos son mutables.
  - Se puede agregar propiedades a los objetos con dot ay bracket notation.

  #### 1.2.5. Exercises
  Write an expression to delete the numWindows property from house.

  ```
  let house = {
    color: 'green',
    numRooms: 4,
    numWindows: 8,
    forSale: false
  };

  delete house.numWindows

  let house = {
    color: 'green',
    numRooms: 4,
    forSale: false
  };
  ```
  <br/>

  Write an expression to add a new hasGarage property to house. 
  Set the value of the hasGarage property to true.

  ```
  house.hasGarage = true;
  ```
  <br/>

  #### 1.2.6. Passing Arguments

  #### 1.2.6.1. Passing a Primitive
  In JavaScript, a primitive (e.g., a string, number, boolean, etc.) is immutable. In other words, any changes made to an argument inside a function effectively creates a copy local to that function, and does not affect the primitive outside 
  of that function. Check out the following example: <br/><br/>

  ```
  function changeToEight(n) {
    n = 8; // whatever n was, it is now 8... but only in this function!
  };
  let n = 7;
  changeToEight(n);
  console.log(n); // 7
  ```
  <br/>

  ```changeToEight()``` takes in a single argument, n, and changes it to 8. However, this change only exists inside the function itself. We then pass the global variable n (which is assigned the value 7) into the function. After invoking it, n is still equal to 7.

  Atention: 
  ```
  let n = { number: 7 };
  function changeToEight(n) {
    n = {
      numero: 8
    };
  };
  changeToEight(n);
  console.log(n); // { number: 7 }
  ```
  <br/>

  Now:
  ```
  var n = { number: 7 };
  function changeToEight(n) {
      n.numero = 8
  };
  changeToEight(n);
  console.log(n);  // { number: 7, numero: 8 }
  ```
  <br/>

  #### 1.2.6.2. Passing an Object
  On the other hand, objects in JavaScript are mutable. If you pass an object into a function, Javascript passes a reference to that object. Let s see what happens if we pass an object into a function and then modify a property:

  ```
  let originalObject = {
    favoriteColor: 'red'
  };

  function setToBlue(object) {
    object.favoriteColor = 'blue';
  }

  setToBlue(originalObject);

  originalObject.favoriteColor;
  // 'blue'
  ```
  <br/>

  In the above example, originalObject contains a single property, favoriteColor, which has a value of 'red'. We pass originalObject into the setToBlue() function and invoke it. After accessing originalObject s favoriteColor property, we see that the value is now 'blue'!<br/>

  How did this happen? Well, since objects in JavaScript are passed by reference, if we make changes to that reference, we re actually directly modifying the original object itself!<br/>

  What's more: the same rule applies when re-assigning an object to a new variable, and then changing that copy. Again, since objects are passed by reference, the original object is changed as well. Let's take a look at this more closely with another example.<br/>

  **When we modify primitives, a local copy is created in the function scope, but globally it still has the same value and that is not possible for us to access the assigned value in the scope.
  JS objects are passed by reference, if we make changes to that reference, we are directly modifying the object itself.
  The same thing happens when we reassign an object to a new variable and then modify that copy.
  Since objects are passed by reference, the original object is also modified, mutates.**

  Consider this iceCreamOriginal object, which shows the amount of ice cream cones each 
  instructor has eaten:

  ```
  const iceCreamOriginal = {
    Andrew: 3,
    Richard: 15
  };
  ```
  <br/>

  Let's go ahead and make assign a new variable to iceCreamOriginal. We ll then check the value of its Richard property:

  ```
  const iceCreamCopy = iceCreamOriginal;
  iceCreamCopy.Richard;
  // 15
  ```
  <br/>

  As expected, the expression iceCreamCopy.Richard; returns 15 (i.e., it is the same value as the Richard property in iceCreamOriginal). Now, let s change the value in the copy, then check the results:

  ```
  iceCreamCopy.Richard = 99;
  iceCreamCopy.Richard;
  // 99

  iceCreamOriginal.Richard;
  // 99
  ```
  <br/>

  Since objects are passed by reference, making changes to the copy (iceCreamCopy) has a direct effect on the original object (iceCreamOriginal) as well. In both objects, the value of the Richard property is now 99.
  <br/><br/>

  #### 1.2.7. Comparing an Object with Another Object
  On the topic of references, let s see what happens when we compare one object with another object. The following objects, parrot and pigeon, have the same methods and properties:

  ```
  const parrot = {
    group: 'bird',
    feathers: true,
    chirp: function () {
      console.log('Chirp chirp!');
    }
  };

  const pigeon = {
    group: 'bird',
    feathers: true,
    chirp: function () {
      console.log('Chirp chirp!');
    }
  };
  ```
  <br/>

  Naturally, one might expect the parrot object and pigeon object to be equal. After all, both objects look exactly the same! Let s compare parrot and pigeon to find out:

  ```
  parrot === pigeon;
  // false
  ```
  <br/>

  What's going on here? As it turns out, the expression will only return true when comparing two references to exactly the same object. Using what we now know about passing objects, let's confirm this. To start off, let s create a new variable, myBird, and assign it to one of the objects above:

  ```
  const myBird = parrot;
  ```
  <br/>

  As we ve just learned, myBird not only refers to the same object as parrot -- they are the same object! If we make any updates to myBird s properties, parrot s properties will be 
  updated with exactly the same changes as well. Now, the comparison will return true:

  ```
  myBird === parrot;
  // true
  ```
  <br/>

  So since pigeon is not the same object as myBird or parrot, any comparisons between myBird 
  and pigeon will return false:

  ```
  myBird === pigeon;
  // false
  ```
  <br/>

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

  ```
  let string = 'orange';
  function changeToApple(string) {
    string = 'apple';
  }

  changeToApple(string);

  console.log(string);
  // Orange
  ```
  <br/>

  Now:
  ```
  let string = 'orange';

  function changeToApple(string) {
    string2 = 'apple';
    return string;
  }

  changeToApple(string);

  console.log(string2);
  // apple
  ```
  <br/>
  

  Consider the following object, oven:
  ```
  const oven = {
    type: 'clay',
    temperature: 400
  };
  ```
  <br/>

  What is the value of oven's temperature property after the following operations?

  ```
  const newOven = oven;
  newOven.temperature += 50;
  // 450
  ```
  <br/>

  #### 1.2.8. Summary
  Objects are commonly created with literal notation, and can include properties that point to functions called methods. Methods are accessed the same way as other properties of objects, and can be invoked the same way as regular functions, except they automatically have access to the other properties of their parent object.<br/>

  By default, objects are mutable (with a few exceptions), so data within them can be altered. <br/>

  New properties can be added, and existing properties can be modified by simply specifying the property name and assigning (or re-assigning) a value. Additionally, properties and methods of an object can be deleted as well with the delete operator, which directly mutates the object.<br/>

  We ve modified objects quite a bit in this section, and even added new methods into them. In the very next section, we ll take a closer look at invoking these methods, as well as how these methods can directly access and modify an object itself!
  <br/><br/>

  #### 1.2.9. Further Research
  
  - The 'delete' operator on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete
  <br/><br/>

  ### 1.3. Functions vs. Methods
  At this point, we ve mostly seen objects with properties that behave more like attributes. 
  That is, properties such as color or type are data that describe an object, but they don't "do" anything. We can extend functionality to objects by adding methods to them.<br/>

  Say that we have a function, sayHello(), which simply logs a message to the console:

  ```
  function sayHello () {
    console.log('Hi there!');
  }
  ```
  <br/>

  Now, say that we also have a developer object with a single property, name:

  ```
  const developer = {
    name: 'Andrew'
  };
  ```
  <br/>

  If we want to add the sayHello() function into the developer object, we can add the same way as we add other new properties: by providing property name, then giving it a value. This time, the value of the property is a function!<br/>

  ```
  developer.sayHello = function () {
    console.log('Hi there!');
  };
  ```
  <br/>

  This is how the updated developer object looks:

  ```
  {
    name: 'Andrew',
    sayHello: function () {
      console.log('Hi there!');
    }
  }
  ```
  <br/>

  So now that a sayHello property has been defined, how do we go about calling (i.e., invoking) its referenced function?
  <br/><br/>

  #### 1.3.1. Calling Methods
  We can access a function in an object using the property name. Again, another name for a function property of an object is a method. We can access it the same way that 
  we do with other properties: by using dot notation or square bracket notation. Let's take a look back at the updated developer object above, then invoke its sayHello() method:

  ```
  const developer = {
    name: 'Andrew',
    sayHello: function () {
      console.log('Hi there!');
    }
  };

  developer.sayHello();
  // 'Hi there!'

  developer['sayHello']();
  // 'Hi there!'
  ```
  <br/>

  Just like calling a function, an object s method is called by adding parentheses at the end of the method s name. Note that both dot notation and square bracket notation return the same result!
  <br/><br/>

  #### 1.3.2. Passing Arguments Into Methods
  If the method takes arguments, you can proceed the same way, too:

  ```
  const developer = {
    name: 'Andrew',
    sayHello: function () {
      console.log('Hi there!');
    },
    favoriteLanguage: function (language) {
      console.log(`My favorite programming language is ${language}`);
    }
  };

  developer.favoriteLanguage('JavaScript');
  // My favorite programming language is JavaScript
  ```
  <br/>

  - Los m??todos como las funciones, para invocarlas es necesario incluir () al final
  - Los m??todos como las funciones, toman argumentos.
  - Un m??todo es una propiedad que apunta a una funci??n.
  <br/><br/>

  Write an expression that invokes the alerter() function in the following array, myArray:

  ```
  const myArray = [ function alerter() { alert('Hello!'); } ];
  myArray[0]();
  ```
  <br/>

  Write an expression that invokes the function referenced by the bell object s ring property:

  ```
  const bell = {
    color: 'gold',
    ring: function () {
      console.log('Ring ring ring!');
    }
  };

  bell.ring();
  ```
  <br/>

  #### 1.3.3. Call Methods by Property Name
  We've been using anonymous functions (i.e., functions without a name) for object methods. However, naming those functions is still valid JavaScript syntax. Consider the following object, greeter:

  ```
  const greeter = {
    greet: function sayHello() {
      console.log('Hello!');
    }
  };
  ```

  Note that the greet property points to a function with a name: sayHello. Whether this function is named or not, greet is invoked the same way:

  ```
  greeter.greet();
  // 'Hello!'
  ```
  <br/>

  Named functions are great for a smoother debugging experience, since those functions will have a useful name to display in stack traces. They re completely optional, however, and you ll often read code written by developers who prefer one way or the other.
  <br/><br/>

  #### 1.3.4. A Method Can Access the Object it was Called On
  Recall that an object can contain data and the means to manipulate that data. But just how can an object reference its own properties, much less manipulate some of those properties itself? This is all possible with the this keyword!

  Using this, methods can directly access the object that it is called on. Consider the following object, triangle:

  ```
  const triangle = {
    type: 'scalene',
    identify: function () {
      console.log(`This is a ${this.type} triangle.`);
    }
  };
  ```
  <br/>

  Note that inside the identify() method, the value this is used. When you say this, what you re really saying is "this object" or "the object at hand." this is what gives the identify() method direct access to the triangle object s properties:

  ```
  triangle.identify();
  // 'This is a scalene triangle.'
  ```
  <br/>

  When the identify() method is called, the value of this is set to the object it was called on: triangle. As a result, the identify() method can access and use triangle s type property, as seen in the above console.log() expression.

  Note that this is a reserved word in JavaScript, and cannot be used as an identifier (e.g. variable names, function names, etc.).

  - _this_ refers to the containing object
  - Using _this_, methods can access and manipulate the properties of the object.
  - The value of _this_ is set when the method is called on an object and that value refers to the object.
  - _this_ is a reserved keyword.

  Let's make sure we re still on the same page! Write an expression that invokes the function referenced by the tree object s growOneFoot property:

  ```
  const tree = {
    type: 'redwood',
    leaves: 'green',
    height: 80,
    age: 15,
    growOneFoot: function () {
      this.height += 1;
    }
  };

  tree.growOneFoot();
  ```
  <br/>

  #### 1.3.4. Exercises
  Create an object called 'chameleon' with two properties:<br/>
  1. 'color', whose value is initially set to 'green' or 'pink'<br/>
  2. 'changeColor', a function which changes 'chameleon''s 'color' to 'pink'<br/>
  if it is 'green', or to 'green' if it is 'pink'.<br/><br/>

  ```
  const chameleon = {
    color: 'pink',
    changeColor: function () {
        if(this.color == 'pink') {
            this.color = 'green';
        } else {
            this.color = 'pink';
        }
    }
  };
  chameleon.changeColor();
  console.log(chameleon.color);
  ```
  <br/>

  
  #### 1.3.5. The value of this
  Depending on how a function is called, this can be set to different values! Later in this course, we ll take a deep dive into different ways that functions can be invoked, and how each approach influences the value of this.
  <br/><br/>

  #### 1.3.6. Summary
  A method is a function property of an object. It is accessed the same way as any other property of the object (i.e., using dot notation or square bracket notation), and is invoked the same way as a regular function outside of an object (i.e., adding parentheses to the end of the expression).<br/><br/>

  Since an object is a collection of data and the means to operate on that data, a method can access the object it was called on using the special this keyword. The value of this 
  is determined when a method is invoked, and its value is the object on which the method was called. Since this is a reserved word in JavaScript, its value cannot be used as an 
  identifier. Feel free to check out the links below for an additional look at methods and their relationship with this.<br/><br/>

  We ve spent a bit of time on this inside objects, but did you know that the value of this can have different meanings outside an object? In the next section, we ll take a close look at globals, their relationship with this, and the implications of using them.
  <br/><br/>

  #### 1.3.7. Further Research
  - Defining Methods on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Defining_methods
  - 'this' in Methods: https://javascript.info/object-methods#this-in-methods
  <br/><br/>

  ### 1.4. Beware of Globals

  #### 1.4.1. Things that Belong to Objects
  Previously, we saw that the properties and methods contained inside an object belong to that object. Let s drive this home with one quick example:

  ```
  const chameleon = {
    eyes: 2,
    lookAround: function () {
      console.log(`I see you with my ${this.eyes} eyes!`);
    }
  };

  chameleon.lookAround();
  // 'I see you with my 2 eyes!'
  ```
  <br/>

  We ve already looked at how this inside a method refers to the object that the method was called on. Let s take a closer look at chameleon s lookAround() method.

  ```
  lookAround: function () {
    console.log(`I see you with my ${this.eyes} eyes!`);
  }
  ```

  Inside the function body is the code this.eyes. Since the lookAround() method was called on the chameleon object as chameleon.lookAround();, the value of this is the chameleon 
  object itself! As such, this.eyes is the number 2, since it refers to the value of the chameleon object s eyes property.

  Now, let s check out a different example. What do you think will be the value of this inside the following code?

  ```
  function whoThis () {
    this.trickyish = true
  }
  whoThis();
  ```
  <br/>

  #### 1.4.2. Write your thoughts below
  What do you think will be the value of this inside the following code? Window object<br/>
  What does the above expression output? Undefined
  <br/><br/>

  #### 1.4.3. this and Function Invocation
  Let s compare the code from the chameleon object with the whoThis() code.

  ```
  const chameleon = {
    eyes: 2,
    lookAround: function () {
      console.log(`I see you with my ${this.eyes} eyes!`);
    }
  };
  chameleon.lookAround();

  function whoThis () {
    this.trickyish = true
  }
  whoThis();
  ```
  <br/>

  #### 1.4.4. this in the Function/Method
  Before we dive into how this all works, take a look at the use of this inside 
  both of these code snippets:

  // from the chameleon code:<br/>
  ```
  console.log(`I see you with my ${this.eyes} eyes!`);
  ```

  // from the whoThis() code:<br/>
  ```
  this.trickyish = true
  ```

  There is some other code around them, but both of them have the format _this.<some-identifier<some-identifier>>_. For our purposes of discovering the value of this, it does not
  matter that in the chameleon code, we re using this to retrieve a property, while in the whoThis() code, we re using this to set a property.

  So, in both of these cases, the use of this is virtually identical.
  <br/><br/>

  #### 1.4.5. Compare the Structures of the Function/Method
  Now, I want you to pay attention to the differences in structure of how the two snippets of code are invoked. The lookAround() code is a method because it belongs to an object. Since it s a method, it s invoked as a property on the chameleon object:

  ```
  chameleon.lookAround();
  ```

  Now compare that with the whoThis() code. whoThis() is not a method; it's a plain, old, 
  regular function. And look at how the whoThis() function is invoked:

  ```
  whoThis();
  ```

  Just like every normal function is invoked; it's just the name of the function and the parentheses (there s no object and no dot in front of it).
  <br/><br/>

  #### 1.4.6. this and Invocation
  How the function is invoked determines the value of this inside the function. ??? That 
  sentence is really important, so read that two more times...we ll wait!<br/><br/>

  Because .lookAround() is invoked as a method, the value of this inside of .lookAround() is whatever is left of the dot at invocation. Since the invocation looks like:

  ```
  chameleon.lookAround();
  ```

  The chameleon object is left of the dot. Therefore, inside the .lookAround() method, this will refer to the chameleon object!

  Now let s compare that with the whoThis() function. Since it is called as a regular function (i.e., not called as an method on an object), its invocation looks like:

  ```
  whoThis();
  ```

  Well, there is no dot. And there is no object left of the dot. So what is the value of this inside the whoThis() function? This is an interesting part of the JavaScript language.
  When a regular function is invoked, the value of this is the global window object.
  <br/><br/>

  #### 1.4.7. The window Object
  If you haven't worked with the window object yet, this object is provided by the browser environment and is globally accessible to your JavaScript code using the identifier, window. 
  This object is not part of the JavaScript specification (i.e., ECMAScript); instead, it is developed by the W3C.

  This window object has access to a ton of information about the page itself, including:

  - The page s URL (window.location;)
  - The vertical scroll position of the page (window.scrollY)
  - Scrolling to a new location (window.scroll(0, window.scrollY + 200); to scroll 200 
  pixels down from the current location)
  - Opening a new web page (window.open("https://www.udacity.com/");)

  ```
  const car = {
    numberOfDoors: 4,
    drive: function () {
      console.log(`Get in one of the ${this.numberOfDoors} doors, and let s go!`);
    }
  };
  const letsRoll = car.drive;
  letsRoll();
  ```
  <br/>

  What does you think this refers to in the code above? The window object
  <br/><br/>

  #### 1.4.8. Global Variables are Properties on window
  Since the window object is at the highest (i.e., global) level, an interesting thing happens with global variable declarations. Every variable declaration that is made at 
  the global level (outside of a function) automatically becomes a property on the window object!<br/>

  Here we can see that the currentlyEating variable is set to 'ice cream'. Then, we immediately see that the window now has a currentlyEating property! Checking this property against the currentlyEating variable shows us that they are identical.

  ```
  var currentlyEating = 'ice cream';
  window.currentlyEating === currentlyEating
  // true
  ```
  <br/>

  #### 1.4.9. Globals and var, let, and const
  The keywords var, let, and const are used to declare variables in JavaScript. var has been around since the beginning of the language, while let and const are significantly newer additions (added in ES6).

  Only declaring variables with the var keyword will add them to the window object. If you declare a variable outside of a function with either let or const, it will not be added as 
  a property to the window object.

  ```
  let currentlyEating = 'ice cream';
  window.currentlyEating === currentlyEating
  // false!
  ```
  <br/>

  #### 1.4.10. Global Functions are Methods on window
  Similarly to how global variables are accessible as properties on the window object, any global function declarations are accessible on the window object as methods:

  ```
  function learnSomethingNew() {
    window.open('https://www.udacity.com/');
  }

  window.learnSomethingNew === learnSomethingNew
  // true
  ```
  <br/>

  Declaring the learnSomethingNew() function as a global function declaration (i.e., it s globally accessible and not written inside another function) makes it accessible to your code as either learnSomethingNew() or window.learnSomethingNew().

  Which of the following variables and functions will be available on the window object?

  ```
  var iceCreamEaten = 1;

  function consume (numberOfGallons) {
    var result = iceCreamEaten + numberOfGallons;
    function updateTotals (newTotal) {
      iceCreamEaten = result;
    }
    updateTotals();
  }
  consume(3);
  ```
  <br/>

  #### 1.4.11. Avoid Globals
  We ve seen that declaring global variables and functions add them as properties to the window object. Globally-accessible code sounds like something that might be super helpful, right? I mean, wouldn t it be great if you could always be within arms reach of some ice cream (or is that just my lifelong dream)?<br/><br/>

  Counterintuitively, though, global variables and functions are not ideal. There are actually a number of reasons why, but the two we ll look at are:
  - Tight coupling
  - Name collisions
  <br/><br/>

  #### 1.4.12. Tight Coupling
  Tight coupling is a phrase that developers use to indicate code that is too dependent on the details of each other. The word "coupling" means the "pairing of two items together.
  " In tight coupling, pieces of code are joined together in a way where changing one unintentionally alters the functioning of some other code:

  ```
  var instructor = 'Richard';
  function richardSaysHi() {
    console.log(`${instructor} says 'hi!'`);
  }
  ```
  <br/>

  In the code above, note that the instructor variable is declared globally. 
  The richardSaysHi() function does not have a local variable that it uses to store the instructor's name. Instead, it reaches out to the global variable and uses that. 
  If we refactored this code by changing the variable from instructor to teacher, this would break the richardSaysHi() function (or we d have to update it there, too!). 
  This is a (simple) example of tightly-coupled code.
  <br/><br/>

  #### 1.4.13. Name Collisions
  A name collision occurs when two (or more) functions depend on a variable with the same name. A major problem with this is that both functions will try to update the variable and or set the variable, but these changes are overridden by each other!

  Let s look at an example of name collision with this DOM manipulation code:

  ```
  let counter = 1;
  function addDivToHeader () {
    const newDiv = document.createElement('div');
    newDiv.textContent = 'div number ' + counter;

    counter = counter + 1;

    const headerSection = document.querySelector('header');
    headerSection.appendChild(newDiv)
  }

  function addDivToFooter() {
    const newDiv = document.createElement('div');
    newDiv.textContent = 'div number ' + counter;

    counter = counter + 1;

    const headerSection = document.querySelector('footer');
    headerSection.appendChild(newDiv)
  }
  ```
  <br/>

  In this code, we have an addDivToHeader() function and a addDivToFooter() function. 
  Both of these functions create a \<div> element and increment a counter variable.

  This code looks fine, but if you try running this code and adding a few \<div>'s to the \<header> and \<footer> elements, you ll find that the numbering will get off! Both 
  addDivToHeader() and addDivToFooter() expect a global counter variable to be accessible to them -- not change out from under them!

  Since both functions increment the counter variable, if the code alternates between calling addDivToHeader() and addDivToFooter(), then their respective \<div>'s will not 
  have numerically ascending numbers. For example, if we had the following calls:

  ```
  addDivToHeader();
  addDivToHeader();
  addDivToFooter();
  addDivToHeader();
  ```
  <br/>

  The developer probably wanted the \<header> to have three \<div> elements with the numbers 1, 2, and 3 and the \<footer> element to have a single \<div> with the number 1. However,   what this code will produce is a \<header> element with three \<div> but with the numbers 1, 2, and 4 (not 3) and a \<footer> element with the number 3...these are very different results. But it s happening because both functions depend on the counter variable and both update it.<br/>

  So what should you do instead? You should write as few global variables as possible. 
  Write your variables inside of the functions that need them, keeping them as close to where they are needed as possible. Now, there are times when you ll need to write global variables, but you should only write them as a last resort.
  <br/><br/>

  ### 1.4.14. Summary
  The window object is provided by the browser and is not part of the JavaScript language or specification. Any global variable declarations (i.e., those that use var) or global 
  function declarations are added as properties to this window object. Excessive use of global variables is not a good practice, and can cause unexpected problems to accurately-written code.

  Whether you re working with the window object, or with an object you create yourself, recall that all objects are made up of key/value pairs. In the next section, we'll check 
  out how to extract these individual keys or values!
  <br/><br/>

  #### 1.4.15. Further Research
  - The window object on MDN: https://developer.mozilla.org/en-US/docs/Web/API/Window
  - The window specification on W3C: https://www.w3.org/TR/html5/browsers.html#the-window-object
  - Globals are Bad: http://wiki.c2.com/?GlobalVariablesAreBad
  - Coupling on Wikipedia: https://bit.ly/2m07ZOj
  - Name Collision on Wikipedia: https://en.wikipedia.org/wiki/Name_collision
  <br/><br/>

  ### 1.5. Extracting Properties and Values

  #### 1.5.1. Object Methods
  Do you remember earlier when we used the Object() constructor function to create (i.e., instantiate) new objects with the new keyword?

  ```
  const myNewFancyObject = new Object();
  ```
  <br/>

  The Object() function actually includes a few methods of its own to aid in the development of your applications. These methods are:

  ```
  Object.keys()
  Object.values()
  ```
  <br/>

  Whether you re building logic in your code, or just writing a utility "helper" function, feel free to use these methods as necessary. Let s see how each of these work!

  ```
  let array = ['a', 'b', 'c', 'd', 'e'];
  console.log(Object.keys(array), Object.values(array));
  // [ '0', '1', '2', '3', '4' ] [ 'a', 'b', 'c', 'd', 'e' ]

  let object = {
    key1: 'value1',
    key2: 'value2',
    key3: 'value3',
    key4: 'value4'
  };

  console.log(Object.keys(object), Object.values(object));
  // [ 'key1', 'key2', 'key3', 'key4' ] [ 'value1', 'value2', 'value3', 'value4' ]<br/>

  let object2 = {
    key1: {
        subkey1: 'subvalue1',
        subkey2: 'subvalue2'
    },
    key2: 'value2',
    key3: 'value3',
    key4: 'value4'
  };

  console.log(Object.keys(object2), Object.values(object2));
  // [ 'key1', 'key2', 'key3', 'key4' ] [{ subkey1: 'subvalue1', subkey2: 'subvalue2' }, 'value2', 'value3', 'value4']
  ```
  <br/><br/>

  #### 1.5.2. Object.keys() and Object.values()
  At its core, an object is just a collection of key/value pairs. What if we want to extract only the keys from an object? Say we have this object representing a real-life dictionary:

  ```
  const dictionary = {
    car: 'automobile',
    apple: 'healthy snack',
    cat: 'cute furry animal',
    dog: 'best friend'
  };
  ```
  <br/>

  Having a collection of just the words (i.e., the dictionary object s keys) may be particularly 
  useful. While we could use a for...in loop to iterate through an object and build our own list 
  of keys, it can get a bit messy and verbose. Thankfully, JavaScript provides an abstraction 
  just for this!

  When Object.keys() is given an object, it extracts just the keys of that object, then returns 
  those keys in an array:

  ```
  Object.keys(dictionary);
  // ['car', 'apple', 'cat', 'dog']
  ```
  <br/>

  So Object.keys() gives returns an array of the provided object s property names. Likewise, if we want a list of the values of an object, we can use Object.values():

  ```
  Object.values(dictionary);
  // ['automobile', 'healthy snack', 'cute furry animal', 'best friend']
  ```
  <br/><br/>

  #### 1.5.3. Support for Object.keys() and Object.values()
  - Object.keys() has been around for quite a long time, so it is fully supported by every 
  browser.
  - Object.values(), on the other hand, is significantly newer. It was officially added to the language specification in 2017. However, just because it s been added to the specification, it necessarily doesn t mean your browser supports it yet!
  
  How do you know if your browser does support Object.values()? Check out the Browser Compatibility table

  What is true about Object.keys()? Select all that apply.
  Object.keys() will return an array of strings and will return them in the same order as they would be when using a for loop.

  What is true about Object.values()? Select all that apply.
  Object.values() will return the items in the same order as when using a for loop. They won't always be strings, because they can have nested objects.
  <br/><br/>

  #### 1.5.4. Summary
  The Object() constructor function has access to several methods to aid in development. To extract property names and values from an object, we can use:

  - Object.keys() returns an array of a given object s own keys (property names). 
  - Object.values() returns an array of a given object s own values (property values).
  <br/><br/>

  #### 1.5.5. Further Research
  - Object.keys() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys
  - Object.values() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values
  - Browser Compatibility: http://tokenposts.blogspot.com.au/2012/04/javascript-objectkeys-browser.html
  <br/><br/>
  
  ### 1.5. Summary
  
  #### 1.5.1. Further Research
  - JavaScript: The Good Parts by Douglas Crockford: http://javascript.crockford.com/
  - JavaScript: The Good Parts via Goodreads: https://www.goodreads.com/book/show/2998152-javascript