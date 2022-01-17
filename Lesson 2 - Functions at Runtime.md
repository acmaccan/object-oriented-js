  # Object-Oriented JavaScript

  ## 2. Functions at Runtime

  ### 2.1. Introduction

  ### 2.2. First-Class Functions
  En JavaScript, las funciones son First-Class Functions. Esto quiere decir que existen ciertos privilegios que no todos los lenguajes tienen. El mismo soporte para distintas estructuras de datos: numbers, strings, objects, arrays, etc.

  Pensemos en un string:
  - Puede ser alojado en una variable
  - Puede ser retornado de una función
  - Puede ser pasado como argumento en una función

  Esto quiere decir, que en JavaScript las funciones de primera clase tienen los mismos privilegios que otras estructuras de datos.

  #### 2.2.1 Función anónima guardada en una constante

  ```
  const myFunction = function(n1, n2){
      return n1 * n2;
  };

  myFunction(2, 4);
  ```
  <br/>

  #### 2.2.2. Función nombrada guardada en una constante

  ```
  const myFunction = function Suma(n1, n2){
      return n1 * n2;
  };

  myFunction(2, 4);
  ```
  <br/>

  #### 2.2.3. Función sólo declarada
  
  ```
  function average(n1, n2, n3){
      return (n1 + n2 + n3) / 3;
  }

  average.length
  //3

  average.name
  //average
  ```
  <br/>

  Como las funciones son objetos también podemos acceder a sus propiedades

  #### 2.2.4. Functions Can Return Functions
  Recordar que una función debe siempre retornar un valor. 
  - De manera explícita, con return statement (e.g., returning a string, boolean, array, etc.)
  - De manera implícita, con return indefinido (e.g., a function that simply logs something to the console), 
  Una función debe siempre retornar un solo valor.

  Como las funciones de primera clase pueden tratarse como cualquier otro valor, ahora sabemos que podemos retornar una función desde otra función. Una función que retorna otra función es conocida como high-order functions.

  ```
  function alertThenReturn() {
    alert('Message 1!');

    return function () {
      alert('Message 2!');
    };
  }
  console.log(alertThenReturn());
  // Solo veremos Message 1!
  ```
  <br/>

  Para ver el return de la segunda función deberíamos estorearlo en una variable:
  
  ```
  const innerFunction = alertThenReturn();
  ```
  <br/>

  Con esto, lo que estamos haciendo, es alojar el resultado de esa función en una variable. Entonces llamando a esa variable podemos acceder a ella.
  
  ```
  innerFunction();
  // alerts 'Message 2!'
  ```
  <br/>

  De todas formas no es necesario alojar la función en una variable para acceder al segundo alert. Podemos acceder a ambos resultados esperados, utilizando doble paréntesis. 
  
  ```
  console.log(alertThenReturn()());
  ```
  <br/>

  #### 2.2.5. Summary
  In the JavaScript language, functions are first-class functions. This means that we can do with functions just about everything that we can do with other elements in JavaScript, such as strings, arrays, or numbers. JavaScript functions can:
  - Be stored in variables
  - Be returned from a function.
  - Be passed as arguments into another function.

  We've seen quite a few examples of the first two in the list, but what about passing a function as an argument into another function? Since this is such an important and common pattern in JavaScript, we'll take a deep dive in the next section!

  #### 2.2.6. Further Research
  - First-class function on Wikipedia: https://en.wikipedia.org/wiki/First-class_function

  ### 2.3. Callback Functions
  Recall that JavaScript functions are first-class functions. We can do with functions just about everything we can do with other values -- including passing them into other functions! 
  A function that takes other functions as arguments (and/or returns a function, as we learned in the previous section) is known as a higher-order function. A function that is passed as an argument into another function is called a callback function.

  We will be focusing on callbacks in this section. Callback functions are great because they can delegate calling functions to other functions. They allow you to build your applications with composition, leading to cleaner and more efficient code.

  ```
  function highOrder(callback){
  }

  function highOrder(){
      return callback(){
      }
  }

  function callAndAdd(n, callbackFunction){
      return n + callbackFunction();
  }

  function returnsThree(){
      return 3;
  }

  callAndAdd(2, returnsThree);
  // 5
  // 2 + 3
  ```
  <br/>

  #### 2.3.1. Array Methods
  Las funciones son pasadas en un array method y llamada por cada elemento dentro del array (el array donde el método fue invocado).

  - forEach()
  - map()
  - filter()

  #### 2.3.2. forEach()
  Toma una función callback e invoca esa función para cada elemento en el array. En otras palabras, permite iterar a través del array, similar usando un for loop.

  ```
  array.forEach(function callback(currentValue, index, array) {
      // function code here
  });
  ```
  <br/>

  La función coallback recibe los argumentos: el array actual, su index y el array completo. Digamos que tenemos una función simple, logIfOdd(), que toma un número simple y muestra en consola si es impar.

  ```
  function logIfOdd(n) {
    if (n % 2 !== 0) {
      console.log(n);
    }
  }

  logIfOdd(2);
  // (nothing is logged)

  logIfOdd(3);
  // 3
  ```
  <br/>

  Ahora qué pasa si queremos chequear todo un array? Podmeos hacerlo a través del forEach y pasar la función logIfOdd como callback.

  ```
  [1, 5, 2, 4, 6, 3].forEach(function logIfOdd(n) {
    if (n % 2 !== 0) {
      console.log(n);
    }
  });

  // 1
  // 5
  // 3
  ```
  <br/>

  #### 2.3.3. map()
  Es similar al forEach. Se invoca una función callback por cada elemento en el array. Sin embargo, map() retorna un nuevo array basado en lo retornado de la función.

  ```
  const names = ['David', 'Richard', 'Veronika'];

  const nameLengths = names.map(function(name) {
    return name.length;
  });
  ```
  <br/>

  Recordar: forEach() no retorna nada, mientras map() retorna un nuevo array con los valores que son retornados desde la función.

  #### 2.3.4. Ejercicio
  
  Using map()
  Using the musicData array and map():
    - Return a string for each item in the array in the following format:
      <album-name> by <artist> sold <sales> copies
    - Store the returned data in a new albumSalesStrings variable
  Note:
    - Do not delete the musicData variable
    - Do not alter any of the musicData content
    - Do not format the sales number leave it as a long string of digits

  ```
  const musicData = [
      { artist: 'Adele', name: '25', sales: 1731000 },
      { artist: 'Drake', name: 'Views', sales: 1608000 },
      { artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
      { artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
      { artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
      { artist: 'Original Broadway Cast Recording', 
        name: 'Hamilton: An American Musical', sales: 820000 },
      { artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
      { artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
      { artist: 'Rihanna', name: 'Anti', sales: 603000 },
      { artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
  ];

  const albumSalesStrings = musicData.map(album =>{
      return album.name + ' by ' + album.artist + ' sold ' + album.sales + ' copies'
  })

  console.log(albumSalesStrings);
  ```
  <br/>

  #### 2.3.5. filter()
  Es similar a map
  - Se llama en un array
  - Toma una función como argumento
  - Retorna un nuevo array

  La diferencia es que la función pasada es usada como test, y sólo los items del array que pasan el test son incluidos en un nuevo array.

  ```
  const names = ['David', 'Richard', 'Veronika'];

  const shortNames = names.filter(function(name) {
    return name.length < 6;
  });
  ```
  <br/>

  De nuevo, la función que es pasada a filter se llama para cada item del array. El primer elemento, 'David', es alojado en la variable name, se performa el test. Si es igual o mayor a 6 es salteado y no incluido en el array. Pero si es menor, es incluido en el nuevo array. 

  Recordar: filter() retorna un nuevo array, no modifica el anterior.

  #### 2.3.6. Ejercicio
  
  Using filter()
  Using the musicData array and filter():
    - Return only album objects where the album s name is 10 characters long, 25 characters long, or anywhere in between
    - Store the returned data in a new 'results' variable
  
  Note:
    - Do not delete the musicData variable
    - Do not alter any of the musicData content

  ```
  const musicData = [
      { artist: 'Adele', name: '25', sales: 1731000 },
      { artist: 'Drake', name: 'Views', sales: 1608000 },
      { artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
      { artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
      { artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
      { artist: 'Original Broadway Cast Recording', 
        name: 'Hamilton: An American Musical', sales: 820000 },
      { artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
      { artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
      { artist: 'Rihanna', name: 'Anti', sales: 603000 },
      { artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
  ];

  const results = musicData.filter(album =>{
      if(album.name.length >= 10 && album.name.length <= 25){
          return album;
      }
  })

  console.log(results);
  ```
  <br/>

  #### 2.3.7. Summary
  Funciones en JS pueden tomar una variedad de diferentes argumentos: strings, números, arrays, objetos. Como las funciones son funciones de primera clase, también pueden ser pasadas como argumentos a una función dada.
  Las funciones que toman otras funciones como argumentos son llamadas funciones de alto orden. Funciones que son pasadas como argumentos a otras funciones son llamadas funciones callback.

  Las callbacks te permiten pasar funciones sin necesidad de nombrarlas (funciones anónimas), lo que lleva a tener menos funciones flotando por ahí. Esto también permite delegar funciones a otras funciones. 

  Los métodos de array como, forEach(), map() y filter() aprovechan los callbacks para ejecutar otras funciones sobre los elementos del array. Hay otros métodos array como: 
  - Create: let fruits = ['Apple', 'Banana']
  - Access: 
    - let last = fruits[fruits.length - 1]
    - let first = fruits[0]
    - let first = fruits.0
    - let fruit = fruits['Apple']
    - Object.keys
    - Object.values
    - indexOf
  - length
  - push
  - pop
  - shift
  - unshift
  - splice
  - slice
  - join
  - find
  - findIndex
  - flat
  - includes
  - reverse
  - sort
  - some
  - every
  - toString
  - Otros

  ### 2.4. Scope

  #### 2.4.1. Block Scope vs. Function Scope
  Esto diferencia hasta donde puede ser vista una variable en el código.
  Los científicos de datos llaman a esto lexical scope.

  También existe otro tipo de scope llamado runtime scope. Cuando una función es ejecutada, se crea un nuevo runtime scope. Este scope representa el contexto de una función, o más específicamente, un set de variables disponibles que dispone la función para utilizar.

  Las funciones tienen acceso a:
  - A los argumentos pasados a la función, sean números, strings u otras funciones.
  - A todas las variables declaradas dentro de la función.
  - A las mismas variables que la función padre use:
    - sus variables locales
    - sus argumentos
    - las variables dentro del scope de la función padre de esa función padre.
  - A las funciones globales.

  #### 2.4.2. Scope
  El runtime scope de una función describe las variables disponibles para el uso dentro de una función dada. El código dentro de la función tiene acceso a:
  - Los argumentos de la función
  - Las variables locales declaradas dentro de esa función
  - Las variables dentro del scope de la función padre
  - Las variables globales

  ```
  const a = 'a'

  function parent(){
    const b = 'b';

    function child(){
      const c = 'c';
    }
  }
  ```
  <br/>

  La función anidada child() tiene acceso a las variables a, b y c. Esto quiere decir que todas están dentro del scope de la función.

  ```
  const myName = 'Andrea';

  function introduceMySelf(){
    const you = 'student';

    function introduce() {
      return `Hello ${you}, I am ${myName}`;
    }
    return introduce();
  }

  console.log(introduceMySelf());
  ```
  <br/>

  #### 2.4.3. Ejercicio

  ```
  const num1 = 5;

  function functionOne() {
    const num2 = 10;
    function functionTwo(num3) {
      const num4 = 35;
      return num1 + num2 + num3 + num4;
    }
    return functionTwo(0);
  }
  ```
  <br/>

  Which variables does functionTwo() have access to? Select all that apply: num1, num2, num3 y num4

  #### 2.4.4. JavaScript is Function-Scoped

  #### 2.4.4.1. Function-Scoping
  Tradicionalmente, las variables son definidas en el scope de una función, en vez de el scope de un bloque. Como al entrar a una función cambiará el scope, todas las variables definidas dentro de la función no estarán disponibles por fuera de ella. Por otro lado, si hay variables deifinidas dentro de un bloque, por ej. un if statement, esas variables estarán disponibles fuera de ese bloque.

  Ejemplo:
  ```
  var globalNumber = 5;

  function globalIncrementer() {
    const localNumber = 10;

    globalNumber += 1;
    return globalNumber;
  }
  ```
  <br/>

  #### 2.4.4.2. Block-Scoping
  ES6 permite scope adicional con las variables con let y const. Estas variables son utilizadas para declarar variables block-scope y reemplazar var. Para saber más:

  - let: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let
  - const: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const
  - Curso: https://www.udacity.com/course/es6-javascript-improved--ud356

  #### 2.4.4.3. Scope Chain
  Cuando sea que el código atente a acceder a variables durante una llamada a una función, el interpreter de JS siemmpre comenzará por mirar las propias variables locales. Si no encuentra ninguna la búsqueda continuará en lo que se llama una scope chain.

  ```
  function one() {
    two();
    function two() {
      three();
      function three() {
        // function three s code here
      }
    }
  }
  one();
  ```
  <br/>

  El scope chain en este caso podemos verlo moverse hacia afuera desde el nivel más anidado. three(), two(), one() y window y de esta manera three() puede acceder a todas las variables, no sólo dentro de one() y two(), sino cualquier función global definida fuera de one().

  ```
    ╔═════════════════════╗
    ║ Child               ║  
    ║ ╔═════════════════╗ ║
    ║ ║ Parent          ║ ║
    ║ ║ ╔═════════════╗ ║ ║
    ║ ║ ║ Global      ║ ║ ║
    ║ ║ ╚═════════════╝ ║ ║
    ║ ╚═════════════════╝ ║
    ╚═════════════════════╝ 

  JS engine begings to look for the variable
                      ↓
  Is the variable defined in the child function? → Value is retrieved
                      ↓
  Is the variable defined in the parent function? → Value is retrieved
                      ↓
  Is the variable defined in the global environment? → Value is retrieved
                      ↓
                  Undefined
  ```
  <br/>
  
  #### 2.4.5. The Global (window) Object
  Recordar que apps JS corren dentro de un ambiente host, por ej. un browser, el host provee un window object,  también conocido como objeto global. Cualquier variable global declarada es accedida como propiedad de este objeto, que representa el nivel más externo de la scope chain.

  #### 2.4.6. Variable Shadowing
  Qué pasa cuando creamos una varibale con el mismo nombre que otra variable en algún lugar de la scope chain? JS no tirará un error o prevendrá que crees otra variable extra. De hecho, la variable con scope local sólo temporalmente ensombrecerá a la variable externa. Esto es llamado variable shadowing.

  ```
  const symbol = '¥';
  function displayPrice(price) {
    const symbol = '$';
    console.log(symbol + price);
  }
  displayPrice('80');
  // '$80'
  ```
  <br/>

  Entonces, si hay superposiciones de nombres en diferentes contextos, se resolverá moviendo la scope chain de adentro hacia afuera. De este modo, todas las variables locales con el mismo nombre que las externas tomarán precedencia por sobre aquellas que estén en un scope más abierto.

  #### 2.4.7. Ejercicio
  What will the console display when myFunction() is called?

  ```
  let n = 2;

  function myFunction() {
    let n = 8;
    console.log(n);
  }

  myFunction();
  // 8
  ```
  <br/>

  #### 2.4.8. Ejercicio
  When the following code runs, what is the output of the first, second, and third logs to the console (respectively)?

  ```
  let n = 8;

  function functionOne() {
    let n = 9;

    function functionTwo() {
      let n = 10;
      console.log(n);  // First log
    }

    functionTwo();

    console.log(n);  // Second log
  }

  functionOne();

  console.log(n);  // Third log

  // 10, 9, 8
  ```
  <br/>

  #### 2.4.9. Summary
  Cuando una función es ejecutrada crea su propio scope. El scope de una función es un set de variables disponibles para su uso dentro de esa función. El scope de una función incluye:
  1. Los argumentos de la función
  2. Variables locales declaradas dentro de la función
  3. Variables dentro de la función padre
  4. Variables globales

  La variables en JS también son function-scoped. Esto quiere decir que las variables declaradas dentro de una función no están disponibles fuera de esa función, aunque variables definidas dentro de bloques, por ejemplo dentro de un if, sí están disponibles fuera de ese bloque.

  Cuando se trata de acceder a variables, el motor JS atravesará la scope chain, primero mirando el nivel más interno, por ejemplo las variables declaradas localmente dentro de una función, luego scopes más externos y llegando al global scope si fuera necesario.

  #### 2.4.10. Further Research
  - Intro to JavaScript (Lesson 5): https://www.udacity.com/course/intro-to-javascript--ud803
  - Douglas Crockfords discussion of block-scoped variables in The Better Parts: https://www.youtube.com/watch?v=Ji6NHEnNHcA&t=26m9s
  - Block Scoping Rules on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block#Description
  - Functions and Function Scope on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions

  ### 2.5. Closures

  #### 2.5.1. Functions Retain Their Scope
  Entonces, cuando un identificador (una variable) es utilizada, el motor de JS comenzará a chequear en busca del valor para ese identificador dentro del scope chain. Puede que ese identificador se encuentre en el scope local, pero si no es encontrado allí, seguirá la búsqueda en el siguiente outer scope. Y nuevamente, si no lo encuentra ahí buscará en el siguiente outer scope. Hasta llegar al scope global, si fuera necesario.

  Identifier lookup y el scope chain son dos herramientas poderosas para una función acceder a identificadores en el código.
  De hecho vamos a hacer algo interesante: crear una función, empaquetarla con algunas variables y guardarla para acceder luego. Si tienes 5 botones en pantalla podríamos escribir 5 diferentes handlers o usar el mismo código 5 veces con difierentes valores.

  ```
  function remember(number){
    return function(){
      return number;
    }
  }

  const returnedFunction = remember(5);
  console.log(returnedFunction());
  ```
  <br/>

  Cuando el motor de JS entra en remember() crea un nuevo scope de ejecución que apunta al scope prioritario de ejecución. Este nuevo scope incluye una referencia al parámetro number, un Number inmutable de valor 5. Cuando el motor alcanza la función anidada, una función expresión, aracha un link al scope de ejecución actual.

  Este proceso de la función de retener el acceso a su scope se llama closure. En este ejemplo, la función anidada cierra sobre number. Una closure puede capturar cualquier número de parámetros y variables que necesita. MDN define un closure como: La combinación de una función y de un ambiente léxico en el cual la función fue declarada.

  Esta definición puede que no tenga mucho sentido si no entiendes el significado de ambiente léxico.
  El ES5 spec refiere al ambiente léxico como: La asociación de identificadores a variables específicas y funciones basadas en la estructura léxica anidada de ECMAScript code.

  En este caso, el lexical environment refiere al código tal como fue escrito en el JS file. Entonces,
  el closure es:
  - Una función en sí misma
  - El código (pero más importante, la scope chain de) donde la función fue declarada.

  Cuando una función es declarada, se agarra a una scope chain. Lo que lo hace interesante es que sigue bloqueada a esa scope chain aún cuando invocamos la función en otro lugar del código.
  Closures nos permiten guardar una snapshot del estado en el momento en el que la función objeto fue   creada.

  #### 2.5.2. Video
  1. Function
  2. Lexical environment

  Cada función tiene su propio closure y su propio scope. Lo que lo hace poderoso es cuando una función   es retornada desde otra función. Esa función es declarada en una función, pero es retornada y corrida   desde fuera de donde fue declarada, manteniendo su acceso a todo el scope en el que fue declarada. 

  #### 2.5.3. Creating a Closure
  Cada vez que una función es definida, un closure es creado para esa función. Estrictamente hablando, cada función tiene closure. Esto es porque las funciones cierran sobre al menos un otro contexto a lo largo del scope chain: el scope global. Como sea, las capacidades de cierre realmente brillan cuando trabajan con funciones anidadas, una función definida dentro de otra función.

  Recordar que una función anidada tiene acceso a las variables fuera de ella. Por lo que hemos aprendido del scope chain, esto incluye las variables del exterior, que encierra la propia función, la función padre.
  Estas funciones anidadas cierran sobre, capturan variables que no fueron pasadas como argumentos o definidas localmente, conocidas como free variables.

  Como vimos en remember() es importante notar que la función mantienen una referencia al scope padre. Si la referencia a esa función todavía es accesible, el scopoe persiste.

  #### 2.5.4. Closures and Scope
  Estos dos conceptos están tan estrechamente relacionados, que estuvimos trabajando con ellos todo el tiempo.

  ```
  const myName = 'Andrew';

  function introduceMyself() {
    const you = 'student';

    function introduce() {
      console.log(`Hello, ${you}, I m ${myName}!`);
    }

    return introduce();
  }

  introduceMyself();
  // 'Hello, student, I m Andrew!'
  ```
  <br/>

  Para recapitular: myName es variable definida fuera de una función, por lo tanto es una variable global en el scope global. En otras palabras, está disponible para ser usada por todas las funciones.

  En el caso de you, es referenciada por introduce() aunque no fue declarada dentro de ella. Esto es posible porque el scope de las funciones anidadas incluye variables declaradas dentro de la función que la anida. 

  Como resultado, introduce() y su ambiente léxico forman un closure. De esta manera introduce() tiene acceso no sólo a la variable global myName sino también a la variable you, que fue declarada en el scope de su función padre, introduceMyself()

  #### 2.5.5. Ejercicio
  What is the output when result(10); is executed?

  ```
  function outerFunction() {
    let num1 = 5;

    return function(num2) {
      console.log(num1 + num2);
    };
  }

  let result = outerFunction();

  result(10);
  // 15
  ```
  <br/>

  #### 2.5.6. Video

  ```
  function myCounter(){
    let count = 0;

    return function(){
      count +=1;
      return count;
    }
  }
  ```
  <br/>

  Tenemos la función myCounter() que utiliza el closure para crear un estado privado.
  Primero, tenemos una variable local, count establecida en 0.
  Luego myCounter retorna una función que incrementa de a 1 y retorna el contador.
  Lo copado de esto, es que la función anidada tiene un estado privado y mutable,
  pero no puede ser accedida externamente porque cierra sobre la variable counter.

  Voy a invocar el contador y guardar el valor en una variable que va a llamar al contador.

  ```
  let counter = myCounter();
  counter();
  ```
  <br/>

  #### 2.5.7. Applications of Closures
  To recap, we ve seen two common and powerful applications of closures:
  - Passing arguments implicitly.
  - At function declaration, storing a snapshot of scope.

  #### 2.5.8. Ejercicio
  Declare a function named 'expandArray()' that:
  - Takes no arguments
  - Contains a single local variable, 'myArray', which points to [1, 1, 1]
  - Returns an anonymous function that directly modifies 'myArray' by
    appending another '1' into it
  - The returned function then returns the value of 'myArray'

  ```
  function expandArray(){
      let myArray = [1, 1, 1];
      
      return function(){
          myArray.push(1)
          return myArray;
      }
  }

  const callArray = expandArray();
  console.log(callArray());
  ```
  <br/>

  #### 2.5.9. Garbage Collection
  JS maneja memoria con una colección automática de basura. Esto quiere decir que cuando la data ya no es referible (no quedan más referencias que apunten a esa data en un código ejecutable) es recolectada y destruida en un punto más adelante en el tiempo. Esto libera recursos, por ej memoria ram, para que la data una vez consumida, los recursos puedan liberarse y reutilizarse.

  #### 2.5.10. Summary
  Closure refiere a la combinación de una función con su ambiente léxico en el cual esa función fue declarada. Cada vez que una función es definida, closure es creado para esa función. 
  Esto es especialmente poderoso en situaciones donde una función es definida dentro de otra función, permitiendo a la función anidada acceder a variables fuera de ella. Las funciones también mantienen enlace con los scopes padres aún si el padre ha vuelto. Esto previene que la data en sus padres sea recolectada como basura.

  #### 2.5.11. Further Research
  - Memory Management on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management
  - Closures on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
  - Lexical Environments in the ES5 spec: http://es5.github.io/#x10.2

  ### 2.5. Immediately-Invoked Function Expressions (IIFE)

  #### 2.5.1. Function Declarations vs. Function Expressions
  Declaration: define una función y no requiere que una variable sea asignada a ella. Simplemente declara una función y no devuelve un valor por sí misma. 

  ```
  function returnHello() {
    return 'Hello!';
  }
  ```
  <br/>

  Expression: retorna un valor. Las expresiones pueden ser anónimas o nombradas y son parte de la sintaxis de otra expresión. Son comunmente asignadas a variables también. 

  ```
  const myFunction = function(){
    return 'Hello!';
  }

  const myFunction = function returnHello(){
    return 'Hello!';
  }
  ```
  <br/>

  IIFE: Una función que es invocada inmediatamente después de su definición.
  Imaginemos la declaración de una función:

  ```
  function logger() {
    console.log('Hello there!');
  }
  ```
  <br/>

  La podemos convertir en expresión rápidamente, envolviéndola entre paréntesis:
  
  ```
  (function logger() {
    console.log('Hello there!');
  });
  ```
  <br/>

  Si le agregamos un par de paréntesisal terminar, la función será llamada justo después de ser definida:
  
  ```
  (function logger() {
    console.log('Hello there!');
  })();
  ```
  <br/>

  #### 2.5.2. Immediately-Invoked Function Expressions: Structure and Syntax

  ```
  (function sayHi(){
    alert('Hi there!');
  })();
  ```
  <br/>

  La estructura sintáctica de esta función puede parecer un poco extraña, pero lo que hicimos fue sólo envolverla entre paréntesis y agregar otro par de paréntesis al final.

  #### 2.5.3. Passing arguments into IIFEs
  
  ```
  (function (name){
      alert(`Hi, ${name}`);
    }
  )('Andrew');
  ```
  <br/>

  El segundo par de paréntesis no sólo ejecuta inmediatamente la función precedente, sino que toma los argumentos que la función pueda necesitar.

  ```
  (function (x, y){
      console.log(x * y);
    }
  )(2, 3);
  // 6
  ```
  <br/>

  #### 2.5.4. IIFEs and Private Scope
  Uno de los usos primarios de las IIFEs es crear scopes privados. Recordar que las variables en JS son tradicionalmente scoped a una función. Sabiendo esto podremos aprovechar el comportamiento de closures para proteger variables o métodos de ser accedidos. 

  ```
  const myFunction = ( // IIFE desde paréntesis hasta el final
      function () { 
          const hi = 'Hi!'; // Var disponible para el retorno de la fc
          return function () { // fc anónima retornada de myFunction
              console.log(hi);
          }
      }
  )();
  ```
  <br/>

  La IIFE es usada para retornar inmediatamente una función. Esta función corre y retorna una función anónima que es almacenada en la variable myFunction.

  La función que retorna captura la variable hi. Esto permite que myFunction mantenga un estado privado y mutable, que no puede ser accedido por fuera de la función. Y más aúm, debido a que la función expresada es llamada inmediatamente, la IIFE envuelve el código de manera que no se ensucia el global scope.

  What is true about immediately-invoked function expressions?
  - IIFEs can be used to create private scope
  - IIFEs are very closely associated with scope and closures
  - There is an alternative syntax for writing an IIFE

  #### 2.5.5. Alternative Syntax for IIFEs
  
  ```
  (function sayHi(){
    alert('Hi there!');
  }
  )();
  // alerts 'Hi there!'
  ```
  <br/>

  Esto funciona bárbaro pero existen otras formas de escribir esto para alcanzar mejores resultados. El cierre del primer set de paréntesis podemos moverlo al final:

  ```
  (function sayHi(){
    alert('Hi there!');
  }());
  // alerts 'Hi there!'
  ```
  <br/>

  Estas son formas estilísticas de ecribir, no hay una forma correcta de hacerlo. Ambos son acercamientos válidos para llegar al mismo resultado y el motor JS seguirá parseándolos como expresiones funcionales, no como declaraciones.
  Douglas Crockford ha mencionado que envolver la unidad entera entre paréntesis ayuda a los lectores a comprender que lo que están viendo es una expresión.

  https://www.youtube.com/watch?feature=player_detailpage&v=taaEzHI9xyY#t=2020s

  #### 2.5.6. IIFEs, Private Scope, and Event Handling
  Vamos a ver otro ejemplo de un IFEE pero esta vez en contexto del manejo de un evento.
  Digamos que queremos crear un botón en una página que alerte al usuario en cada otro click.
  Una forma de hacer esto, podría ser trackear el número de veces que un botón fue clickeado.
  Pero cómo mantenemos esta data?

  Podríamos trackear el contador con una variable que declaramos en el scope global, esto tiene sentido si otra parte de la app necesita acceder a esa data. De todas formas, un mejor approach sería encapsular esta data en un manejador de eventos en sí.

  Por un lado, porque esto prevendría de polucionar el ambiente global con variables extras (y potencialmente colisiones de nombres de variables). Y es más, si usamos una IIFE podemos aprovechar el cierre para proteger el contador de ser accedido externamente. Esto prevendría cualquier mutación accidental o efectos colaterales no queridos por alterar el contador inadvertidamente.

  ```
  <!-- button.html -->
  <html>
    <body>
      <button id='button'>Click me!</button>
      <script src='button.js'></script>
    </body>
  </html>

  // button.js
  const button = document.getElementById('button');

  button.addEventListener('click', (function() { // Función que retorna una función
    let count = 0; // Creamos una variable local

    return function() { // Retornamos una función
      count += 1; // Incrementa count

      if (count === 2) { // Pero, cuando llega a 2
        alert('This alert appears every other press!'); // Alerta al usuario 
        count = 0; // Y vuelve el contador a cero
      }
    };
  })());
  ```
  <br/>

  Lo que es importante para notar es que la función retornada se cierra sobre la variable count. Esto es porque la función mantiene una referencia sobre el ambiente padre. count está disponible para la función retornada para su uso. Como resultado inmediatamente invocamos una función que retorna esa función. Y como la función retornada tiene acceso a la varibale interna count, un ambiente privado es creado, efectivamente protegiendo la data.

  #### 2.5.7. Ejercicio
  
  ```
  (function(n){
      delete n;
      return n;
  })(2);
  // 2
  ```
  <br/>

  Este puede ser un poco tramposo. La clave en este ejercicio es el operador delete. Este operador sólo es efectivo sobre propiedades de objetos, no puede ser usado para desasignar recursos directamente. No tiene efecto sobre variableso nombre de funciones. Es por eso que este ejercicio tiene 2 como resultado.

  #### 2.5.8. Benefits of Immediately-Invoked Function Expressions
  Como hemos visto, usando funciones expresivas inmediatamente invocadas crea ambientes privados que protegen las variables o métodos de ser accedidos. IIFEs, por último, usan funciones retornadas para acceder a data privada que se encuentra dentro del cierre. Esto funciona muy bien, mientras estas funciones son retornadas para acceso público, aún mantienen la privacidad para las variables declaradas dentro de ellas. 

  Otra gran oportunidad para usar las IIFEs es cuando quieren ejecutar cierto código sin crear variables globales extra. Sin embargo, notemos que una IIFE se espera que sólo sea invocada una vez, para crear un único contexto de ejecución. Si tenemos un código que esperamos volver a utilizar, declarar la función y luego invocarla sería la mejor opción.

  Si tienes una tarea de una sóla vez, como ser inicilizar la aplicación, an IIFE es una gran manera de hacerlo sin polucionar el ambiente global con variables extras. Mantener limpio el espacio de nombres globales reduce la posibilidad de colisiones con nombres de variables duplicadas, etc.

  #### 2.5.9. Summary
  Una IIFE es una función llamada inmediatamente luego de que es definida. Su utilización permite ambientes privados, lo que mantiene la privacidad de las variables definidas dentro de ellas. Esto permite mantener el ambiente global limpio.

  #### 2.5.10. Further Research
  - Function Declarations vs. Function Expressions: https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/
  - An Introduction to IIFEs - Immediately Invoked Function Expressions on A Drip of JavaScript: http://adripofjavascript.com/blog/drips/an-introduction-to-iffes-immediately-invoked-function-expressions.html
  - Immediately-Invoked Function Expression (IIFE) by Ben Alman: http://benalman.com/news/2010/11/immediately-invoked-function-expression/

  ### 2.6. Summary
  - First-Class Functions
  - Functions as values
  - High-order Functions
  - Callback Functions
  - Functions as arguments
  - Scopes
  - Closures
  - Scope-chains
  - IIFEs
