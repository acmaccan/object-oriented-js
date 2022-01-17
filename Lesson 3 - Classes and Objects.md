
  # Object-Oriented JavaScript
  
  ## 3. Class and Objects
  
  #### 3.1.1. Introducción
  Hasta ahora construimos one off objects (objetos únicos). Para construir aplicaciones más estructuradas necesitamos saber cómo construir clases o categorías de objetos.

  En esta sección veremos:
  - cómo crear nuevos objetos con funciones constructoras
  - el uso de this para crear y acceder a propiedades de objetos
  - prototypal inheritance and subclassing

  #### 3.1.2. Propiedades y Métodos
  Como un objeto puede representar data y funcionalidades, podemos usar un objeto para expresar
  cosas reales, personas u objetos, en código.
  
  #### 3.1.3. Ejercicio libre
  
  ```
  let lamp = {
    type: 'desktop',
    color: 'grey',
    light: 'soft',
    state: 'on',
    switch: function(){
      if(this.state === 'off'){
        return this.state = 'on'
      } else { 
        return this.state = 'off'
      }
    }
  }

  console.log(lamp.switch());
  ```
  <br/>

  #### 3.1.4. Ejercicio
  Mirar objetos alrededor y ver cómo sería mejor clasificarlos y agruparlos.

  Decoración:
    Cuadros
    Lámapara
    Escritorio
    Silla
    Espejo
    Biblioteca
    Cajonera
  
  Libros

  Plantas:
    Pothus

  Arte:
    Instrumentos musicales:
      Guitarra

    Materiales pintura:
      Bastidores
      Acrílicos
      Pinceles
  
  Estudios:
    Apuntes
    Fotocopias
    Libros

  Dispositivos electrónicos:
    Compu
    Celu

  #### 3.1.5. Summary
  Los objetos en JS representan cosas de la realidad. 
  Tienen propiedades para representar atributos.
  Tienen métodos para representar acciones que pueden realizar.
  Podemos pensar los objetos como sustantivos: dog / car
  Los valores de las propiedades como adjetivos: blue
  Y los métodos como verbos: drive / bark

  ### 3.2. Constructor Functions
  Hay tres formas de crear un objeto:
  - utilizando literal notation
  - creando una función que retorne un objeto
  - utilizando una función constructora

  Una función constructora es similar a una función que retorna un objeto pero tiene algunas
  diferencias:
  1. Una función constructora comienza con mayúscula
  2. Una función constructora siempre debe llamarse con la keyword new
  3. Mientras una función regular debe crear el objeto que va a retornar y modificarlo 
  directamente, la función constructora crea su objeto automáticamente. Luego para agregar 
  propiedades o método a ese objeto tenemos que utilizar this 

  Para instanciar un nuevo objeto utilizamos el operador new para invocar la función:
  new SoftwareDeveloper();

  El que el nombre del objeto comience en mayúscula, es una convención entre desarrolladores,
  no es un requisito del lenguaje.

  Lo que a una función constructora la determina como tal es:
  - El uso del operador new para invocar la función
  - Cómo la función está escrita internamente

  #### 3.2.1. Constructor Functions: Structure and Syntax
  internamente se ve así:

  ```
  function SoftwareDeveloper() {
    this.favoriteLanguage = 'JavaScript';
  }
  ```
  <br/>

  A diferencia de las variables en las funciones constructoras la persistencia de datos se
  hace con this.
  La función de arriba agregará favoriteLanguage al objeto que crea, y asigna como valor
  por defecto 'JavaScript'.
  this refiere al objeto que fue creado usando new frente a la función constructora. 
  Las funciones constructoras no retornar valores, no retornan nada explícitamente, no deben
  tener un return statement.

  #### 3.2.2. Creating a New Object
  
  ```
  function SoftwareDeveloper(){
    this.favoriteLanguage = 'JavaScript';
  }

  let developer = new SoftwareDeveloper();

  console.log(developer);

  Retorna 
  ▼ SoftwareDeveloper { favoriteLanguage: 'JavaScript' }
    ▼ __proto__: 
      ▶ constructor: ƒ SoftwareDeveloper()
  ```
  <br/>

  Hacemos otro con literal notation y comparamos lo que retorna:

  ```
  let otherDeveloper = { favoriteLanguage: 'JavaScript' };
  
  console.log(otherDeveloper);

  Retorna 
  ▼ { favoriteLanguage: 'JavaScript' }
    ▼ __proto__: 
      ▶ constructor: ƒ Object()
  ```
  <br/>

  #### 3.2.3. Creating Multiple Objects

  Podemos utilizar la misma función constructora como querramos. Invoquemos la función
  algunas veces más, para crear nuevos objetos:

  ```
  let engineer = new SoftwareDeveloper();
  let programmer = new SoftwareDeveloper();

  console.log(engineer);
  // SoftwareDeveloper { favoriteLanguage: 'JavaScript' }
  console.log(programmer);
  // SoftwareDeveloper { favoriteLanguage: 'JavaScript' }
  ```
  <br/>

  #### 3.2.4. Constructor Functions Can Have Parameters
  Uno de los beneficios de las funciones constructoras es que aceptan argumentos. 
  Actualicemos el constructor para que acepte un argumento y asignémosle la propiedad 
  name.

  ```
  function SoftwareDeveloper(name){
    this.favoriteLanguage = 'JavaScript';
    this.name = name;
  }

  let instructor = new SoftwareDeveloper('Andrew');
  console.log(instructor);
  // SoftwareDeveloper { favoriteLanguage: 'JavaScript', name: 'Andrew' }

  let teacher = new SoftwareDeveloper('Richard');
  console.log(teacher);
  // SoftwareDeveloper { favoriteLanguage: 'JavaScript', name: 'Richard' }
  ```
  <br/>

  #### 3.2.5. Preguntas
  Which of the following about constructor functions are true? 
  - must be invoked with new
  - are used to instantiate a new object

  What happens if a constructor function begins with a lower-case letter?
  - Nothing, it will still work.

  ### 3.2.6. Ejercicio
  Declare a 'Sandwich' constructor function that takes three parameters:
  1. 'bread' (string) - the type of bread for the sandwich (e.g. "Wheat")
  2. 'meat' (array) - the meats to put on the sandwich (e.g. '[]' for a vegetarian sandwich!)
  3. 'vegetables' (array) - the vegetables to include in the sandwich

  ```
  function Sandwich(bread, meat, vegetables){
      this.bread = bread;
      this.meat = meat;
      this.vegetables = vegetables;
  }

  let lomitoCompleto = new Sandwich('Pan negro', ['lomito ahumado', 'queso'], ['tomate', 'lechuga']);

  console.log(lomitoCompleto);

  Sandwich {
  bread: 'Pan negro',
  meat: [ 'lomito ahumado', 'queso' ],
  vegetables: [ 'tomate', 'lechuga' ] } 
  ```
  <br/>

  #### 3.2.7. Omitting the new Operator
  Qué pasaría si inadvertidamente invocás un constructor sin el operador new? El objeto
  no se crearía, la función sería invocada como cualquier otra función regular y lo 
  retornado será undefined y el valor de this es completamente diferente.

  ```
  function SoftwareDeveloper(name) {
    this.favoriteLanguage = 'JavaScript';
    this.name = name;
  }

  let coder = SoftwareDeveloper('David');

  console.log(coder);
  // undefined
  ```
  <br/>

  #### 3.2.8. Seeing the Object s Constructor (instanceof)

  ```
  function Developer(name){
    this.name = name;
  }

  const dev = new Developer('Andrea');

  typeof dev;
  "Object" // Nos confirma que es un objeto

  dev instanceof Developer;
  true // Nos confirma que dev es una instancia de Developer
  ```
  <br/>

  #### 3.2.9. instanceof and the Prototype Chain
  En el ejemplo anterior resulta sencilla la confirmación de dev como instancia de Developer porque está directamente instanciado.
  Cuando se tratan de cadenas de prototipos el test puede dificultarse, chequeará si el constructor aparece o no en la cadena de prototipos, pero no sabremos siempre exactamente qué constructor es el que creó el objeto, pero sí nos podrá decir a qué propiedades y métodos ese objeto tendrá acceso.

  #### 3.2.10. Ejercicio
  
  ```
  function Finch(name) {
    this.kingdom = 'Animalia';
    this.name = name;
  }

  function Sparrow(name) {
    this.kingdom = 'Animalia';
    this.name = name;
  }

  const atticus = new Finch('Atticus');
  const jack = new Sparrow('Jack');

  What is the result when atticus instanceof Sparrow; // false
  ```
  <br/>

  #### 3.2.11. Summary
  El sistema de clases de JS se construye directamente sobre el uso de funciones y objetos. Llamando a una función constructora con el operador new podemos instanciar nuevos objetos. El mismo constructor podemos utilizarlo para crear diferentes objetos.

  #### 3.2.12. Further Research
  - The new operator on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new
  - The instanceof operator on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof

  ### 3.3. The 'this' keyword
  Functions ⇔ Objects ⇔ this
  Cuando una función es llamada la variable this es seteada a un objeto específico.
  El valor de this va a depender cómo fue llamada la función.
  Vamos a ver diferentes formas de llamar funciones y ver cómo se comporta this.

  #### 3.3.1. this in Constructor Functions

  ```
  function Cat(name) {
    this.name = name;
    this.sayName = function () {
      console.log(`Meow! My name is ${this.name}`);
    };
  }

  const bailey = new Cat('Bailey');
  ```
  <br/>

  #### 3.3.2. When is this Assigned?
  Uno de los errores más comunes es creer que this refiere al objeto en el que fue creado.
  En realidad no es asignado a nada hasta que el método es llamado, donde this sea usado.
  El valor asignado a this se basa en el objeto que invoca el método donde this es definido.

  ```
  const dog = {
    bark: function () {
      console.log('Woof!');
    },
    barkTwice: function () {
      this.bark();
      this.bark();
    }
  };
  dog.bark();
  // Woof!

  dog.barkTwice();
  // Woof!
  // Woof!
  ```
  <br/>

  Cuando llamamos a this.bark o this.barkTwice, this se setea. Como this puede acceder al 
  objeto que lo creó, barkTwice también puede acceder al objeto dog.
  Qué pasa si sólo escribimos bark() sin this en barkTwice? Buscará una variable local con
  ese nombre y no la encontrará, la buscará en el siguiente outer scope, no lo encontrará.

  #### 3.3.3. Ejercicio
  What is true about _this_? Select all that apply:
  - Using _this_, methods can access and manipulate an object's properties
  - _this_ is a reserved word in JavaScript

  Consider the following constructor function, City:
  ```
  function City(name, population) {
    this.name = name;
    this.population = population;

    this.identify = function () {
      console.log(`${this.name} s population is ${this.population}.`);
    };
  }

  const sanFrancisco = new City('San Francisco', 870000);
  ```
  <br/>

  What is the value of _this_?
  - City NO
  - El objeto recién creado, referenciado por San Francisco SI

  #### 3.3.4. What Does this Get Set To?
  Entonces, this en diferentes contextos:
  - dentro de un método
  - siendo referenciado por una función constructora

  Hay cuatro formas de llamar funciones y cada una de ellas setea this de manera diferente:
  1. Llamando a una función constructora con new, this se setea dentro del objeto nuevo, 
  recién creado. Es decir, no apunta a City, sino a San Francisco.

  2. Al llamar a una función que pertenece a un objeto, un método, setea el this
  al objeto mismo. El método barkTwice() tenía acceso a las propiedades de dog en sí misma.

  3. Llamando a una función por sí misma, invocando a la función regular, seteará this a
  window, que es el objeto global en el ambiente del browser host.

  ```
  function funFunction() {
    return this;
  }

  funFunction();
  // (returns the global object, `window`)
  ```
  <br/>

  4. Permite setear this nosotros mismos. 

  ╔═══════════════╦═════════════╦══════════════════╦═══════════════╦═══════════════╗
  ║ Call Style    ║ 'new'       ║ method           ║ function      ║ custom        ║
  ╠═══════════════╬═════════════╬══════════════════╬═══════════════╬═══════════════╣
  ║ 'this'        ║ {}          ║ object itself    ║ global object ║               ║     
  ╠═══════════════╬═════════════╬══════════════════╬═══════════════╬═══════════════╣
  ║ Example       ║ new Cat()   ║ bailey.sayName() ║ introduce()   ║               ║
  ╚═══════════════╩═════════════╩══════════════════╩═══════════════╩═══════════════╝ 

  #### 3.3.5. Ejercicio

  ```
  const building = {
    floors: 5,
    addFloor: function () {
      this.floors += 1;
    }
  };

  building.addFloor();
  // this is pointing to building
  ```
  <br/>

  ```
  function myFunction() {
    console.log("What is the value of 'this'?");
  }

  myFunction();
  // the value of this is window
  ```
  <br/>

  #### 3.3.6. Summary
  Funciones, objetos y this están todos interconectados. Cuando invocamos un constructor
  con el operador new, una variables this se setea al objeto nuevo recién creado.
  Cuando invocamos un método, this es seteado para el objeto en sí mismo.
  Y cuando invocamos una función en el ambiente navegador, this es seteado a window, el
  objeto global.

  #### 3.3.7. Further Research
  - The this operator on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this

  ### 3.4. Setting our own _'this'_
  Para setear el valor de this nosotros mismos, JS nos ofrece algunos métodos para hacerlo.
  - call() - method on a function
  - apply() - method on a function
  - bind() - method thar returns a new function
  
  Son utilizados en diferentes contextos.
  
  #### 3.4.1. More Ways to Invoke Functions
  call() y apply()
  Cada método puede ser directamente invocado sobre una función en sí misma. Como resultado,
  la función que recibe será invocada con un valor this específico, tanto como cuantos 
  argumentos le sean pasados.

  #### 3.4.2. call()
  Es un método directamente invocado sobre una función. Primero pasamos en él un valor para
  setear el valor de this. Después le pasamos en cualquiera de las funciones receptoras, los
  argumentos, uno a uno, separados por comas.

  ```
  function multiply(n1, n2) {
    return n1 * n2;
  }

  multiply(3, 4);
  // 12

  multiply.call(window, 3, 4);
  // 12
  ```
  <br/>

  - Invocamos el método call directamente sobre multiply()
  - No es seguido de paréntesis
  - call() manejará la invocación y sus argumentos
  - El primer argumento es el valor seteado a this
  - Los otros argumentos son los que toma la función multiply(), individualmente separados por comas

  Cómo invocamos funciones attach a objetos? Al usar call() para invocar métodos nos permite pedir prestado un método de un objeto para ser utilizado en otro objeto.

  ```
  const mockingbird = {
    title: 'To Kill a Mockingbird',
    describe: function () {
      console.log(`${this.title} is a classic novel`);
    }
  };

  mockingbird.describe(); // 'To Kill a Mockingbird is a classic novel'

  const pride = {
    title: 'Pride and Prejudice'
  };

  mockingbird.describe.call(pride); // 'Pride and Prejudice is a classic novel'
  ```
  <br/>

  - call() invoca mockingbird.describe que apunta a una función
  - El valor de this es pasado dentro de call(): pride
  - mockingbird.describe referencia this.title, por lo que necesitamos acceder a la 
  propiedad title del objeto al que hace referencia this.
  - Como seteamos nuestro propio valor de this, el valor de this.title será accedido
  desde el objeto pride.

  call() nos sirve para los casos en que buscamos invocar una función en el scope del
  primer argumento que le pasamos.

  #### 3.4.3. apply()
  En vez de pasar los argumentos separados por coma, apply recibe un array.

  ```
  function multiply(n1, n2) {
    return n1 * n2;
  }
  multiply.call(window, 3, 4); // 12
  multiply.apply(window, [3, 4]); // 12
  ```
  <br/>

  El primer argumento sigue siendo el valor a setear para this. Ahora qué pasa con los métodos y objetos?

  ```
  const mockingbird = {
    title: 'To Kill a Mockingbird',
    describe: function () {
      console.log(`${this.title} is a classic novel`);
    }
  };

  const pride = {
    title: 'Pride and Prejudice'
  };
  
  mockingbird.describe.call(pride); // 'Pride and Prejudice is a classic novel'
  mockingbird.describe.apply(pride); // 'Pride and Prejudice is a classic novel'
  ```
  <br/>

  Both approaches produce the same result.

  #### 3.4.4. Choosing One Method Over the Other
  call() puede limitarnos cuando no sabemos la cantidad de argumentos que necesita
  la función. En este caso apply() será una mejor opción. Desempaca los argumentos
  en el array y los pasa.

  Tenemos un objeto
  ```
  let cat = {
    name: 'Bailey'
  }
  ```
  <br/>
  
  Y una función con un valor _this_
  ```
  function sayHello(message){
    console.log(`${message}, ${this.name}`)
  }

  sayHello.call(cat, 'Hi'); // Hi, Bailey
  sayHello.apply(cat, ['Hello']); // Hello, Bailey
  ```
  <br/>

  #### 3.4.5. Ejercicio

  ```
  const dave = {
    name: 'Dave'
  };

  function sayHello(message) {
    console.log(`${message}, ${this.name}. You re looking well today.`);
  }
  ```
  <br/>

  Let's say you want the message 'Hello, Dave. You re looking well today.' printed to the console. 
  
  ```
  sayHello.apply(dave, ['Hello']);
  ```
  <br/>

  #### 3.4.6. Ejercicio
  Consider the following Andrew and Richard objects:

  ```
  const Andrew = {
    name: 'Andrew',
    introduce: function () {
      console.log(`Hi, my name is ${this.name}!`);
    }
  };

  const Richard = {
    name: 'Richard',
    introduce: function () {
      console.log(`Hello there! I'm ${this.name}.`);
    }
  };
  ```
  <br/>

  When Richard.introduce.call(Andrew) is executed, what is logged to the console?

  ```
  Hello there! I'm Andrew.
  ```
  <br/>

  #### 3.4.7. Ejercicio
  
  ```
  const andrew = {
    name: 'Andrew'
  };

  function introduce(language) {
    console.log(`I'm ${this.name} and my favorite programming language is ${language}.`);
  }
  ```
  <br/>

  Write an expression that uses the call() method to produce the message: 
  'I'm Andrew and my favorite programming language is JavaScript.'

  ```
  introduce.call(andrew, 'JavaScript');
  ```
  <br/>

  #### 3.4.8. Callbacks and this
  Con callbacks se vuelve un poco tricky. 

  ```
  function invokeTwice(cb) {
    cb();
    cb();
  }

  const dog = {
    age: 5,
    growOneYear: function () {
      this.age += 1;
    }
  };

  dog.growOneYear();  // this works as expected 5 to 6
  dog.age; // 6

  invokeTwice(dog.growOneYear); // undefined
  dog.age; // 6
  ```
  <br/>

  Esto pasa porque this hace referencia al objeto window.

  #### 3.4.9. Saving this with an Anonymous Closure
  Cuando pasamos como argumento growOneYear la estamos pasando como función y no como método. Esto hace que el this tenga valor window y no dog, como quisiéramos.

  #### 3.4.10. Saving this with an Anonymous Closure
  Una forma de resolver esto es usando un closure anónimo sobre el objeto dog:

  ```
  invokeTwice(function () { 
    dog.growOneYear(); 
  });

  dog.age; // 7
  ```
  <br/>

  #### 3.4.11. Saving this with bind()
  Como este es un patrón común, JS nos provee el método bind(). Es similar a call y apply, pero nos permite definir directamente un valor para this. Es un método que también se llama sobre una función, pero a diferencia de los otros, bind retorna una nueva función quem cuando es llamada, tiene this con el valor que le hemos seteado.

  ```
  function invokeTwice(cb) {
    cb();
    cb();
  }

  const dog = {
    age: 5,
    growOneYear: function () {
      this.age += 1;
    }
  };

  invokeTwice(dog.growOneYear); 
  // Esto nos devolverá undefined porque growOneYear apunta al objeto window

  const myGrow = dog.growOneYear.bind(dog); 
  // A través de bind seteamos el valor de this para cuando utilicemos growOneYear
  // Esto retorna una nueva función que hace que growOneYear ahora haga referencia al objeto dog
  // y ya no a window

  invokeTwice(myGrow);
  // Funcionaría como el clousure anónimo

  dog.age; // 7
  ```
  <br/>

  #### 3.4.12. Question
  What is true about bind()?
  - bind() is a method that is called on a function
  - bind() returns a new function that, when called, has this set to the provided object

  #### 3.4.13. Ejercicio
  Consider the following:

  ```
  const driver = {
    name: 'Danica',
    displayName: function () {
      console.log(`Name: ${this.name}`);
    }
  };

  const car = {
    name: 'Fusion'
  };
  ```
  <br/>

  Write an expression using bind() that allows us to "borrow" the displayName() method from driver for the car object to use. Note: The expression itself is sufficient (no need to save it to a variable).

  ```
  driver.displayName.bind(car);
  ```
  <br/>

  #### 3.4.14. Summary
  JS nos provee de tres métodos que nos permiten setear el valor de this para una función:
  - call() invoca la función y sus argumentos, pasados individualmente separados por comas.
  - apply() invoca la función y sus argumentos, pasados en un array.
  - bind() retorna una nueva función con this conectado a un objeto específico, permitiéndonos llamarla como una función regular.

  #### 3.4.15. Further Research
  - Kyle Simpson s You Don t Know JS: https://github.com/getify/You-Dont-Know-JS/blob/master/this%20&%20object%20prototypes/README.md#you-dont-know-js-this--object-prototypes
  - call() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call
  - apply() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply
  - bind() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind

  ### 3.5. Prototypal Inheritance
  Herencia o extensión, un objeto puede recibir las características de otro objeto.

  ```
  Car() → Prototype → new → car1 → red
                    ↘ new → car2 → blue
                    ↘ new → car3 → green
  ```
  <br/>

  No sólo cada uno tiene sus propias propiedades, sino que estan ligadas a un objeto común llamado prototipo. Nosotros podemos agregar métodos al prototipo para que todos los new car puedan compartir.
  En vez de compartir un nuevo método para cada vez que un car es creado, cada car puede compartir el mismo. En JS podemos aprovechar los prototipos para manejar la herencia.

  #### 3.5.1. Adding Methods to the Prototype
  Recordemos que los objetos contienen data, propiedades. Así como los medios para manipular esa data, métodos.

  ```
  function Cat(name) {
    this.lives = 9;
    this.name = name;

    this.sayName = function () {
      console.log(`Meow! My name is ${this.name}`);
    };
  }
  ```
  <br/>

  De esta manera el método sayName se agrega a todos los objetos Cat guardando la función al atributo sayName al objeto recién creado con new desde Cat.

  Esto funciona muy bien, pero qué pasa si queremos instanciar más de un objeto Cat con este constructor? Crearíamos una nueva función por cada vez que se instancie ese objeto. Es más, si quisieras realizar modificaciones sobre el objetom tendrías que modificar cada objeto individualmente. En esta situación tiene sentido tener creados todos los objetos desde el mismo constructor Cat que compartan el mismo método.

  Para ahorrar memoria y mantener las cosas limpias podemos agregar métodos al prototipo de la función constructora Cat. El prototipo es sólo un objeto y todos los objetos creados por una función constructora mantienen una referencia al prototipo. Esos objetos incluso pueden utilizar las propiedades del prototipo como si fueran suyas.

  JS aprovecha este enlace secreto entre el objeto y su prototipo para implementar la herencia. Consideremos la siguiente cadena prototípica:

  ```
                          ╔═════════════════╗  ╔═════════════════╗  ╔═════════════════╗
                          ║   constructor   ║  ║   constructor   ║  ║   constructor   ║
  ╔═══════════════╗  new  ╠═════════════════╣  ╠═════════════════╣  ╠═════════════════╣
  ║    bailey     ║   ↵   ║       Cat()     ║  ║     Animal()    ║  ║     Object()    ║
  ╠═══════════════╣       ╚═════════════════╝  ╚═════════════════╝  ╚═════════════════╝ 
  ║    lives      ║                ┋                    ┋                    ┋           ╔═════════════════╗
  ╚═══════════════╝       ╔═════════════════╗  ╔═════════════════╗  ╔═════════════════╗  ║    undefined    ║    
          ╹               ║    prototype    ║  ║    prototype    ║  ║    prototype    ║  ╚═════════════════╝
          ╹               ╠═════════════════╣  ╠═════════════════╣  ╠═════════════════╣           ╹
          ┗╺╺╺╺╺╺╺╺╺╺╺╺╺╺ ║      meow()     ║╺╺║     kingdom     ║╺╺║ hasOwnProperty()║╺╺╺╺╺╺╺╺╺╺╺┛ 
                          ║                 ║  ║  calculateAge() ║  ║ isPrototypeOf() ║
                          ╚═════════════════╝  ╚═════════════════╝  ╚═════════════════╝ 
  ```

  - Cat() constructor is invoke using new operator
  - new operator creates the bailey instance object
  - meow() method is defined in the prototype of bailey object s constructor function
  - prototype is just an object 
  - all objects created by that constructor are secretly linked to the prototype
  - podemos ejecutar bailey.meow() como si fuera su propio método

  Recordemos que cada función tiene una propiedad prototipo, que realmente es sólo un objeto.  
  Cuando una función es invocada como un constructor usando el operador new, crea y retorna un nuevo objeto.
  Este objeto está secretamente enlazado al prototipo de su constructor.
  Este enlace es el que le permite ustilizar propiedades y métodos del prototipo como si fueran propios.

  Como sabemos que la propiedad de un prototipo sólo apunta a un objeto regular, ese objeto en sí mismo tiene también un enlace secreto a su prototipo. Y ese prototipo objeto también tiene una referencia a su propio prototipo, y así sucesivamente. Así es cómo la cadena prototípica es formada.

  #### 3.5.2. Finding Properties and Methods on the Prototype Chain
  Ya sea que estés queriendo acceder a una propiedad o a un método el intérprete de JS buscará por ellos a lo largo de la cadena prototípica en un orden muy particular:
  - Primero, buscará en las propiedades propias del objeto. Esto quiere decir que si propiedades o métodos fueron definidos en directamente en el objeto mismo esto tomará precedencia sobre cualquier otra propiedad o método en otro lado, si sus nombres son los mismos, similar a shadowing en la scope chain.
  - Si no encuentra, buscará en el prototipo del constructor del objeto para matchear.
  - Si no existe en el prototipo, seguirá buscando en la cadena.
  - Al final de la cadena buscará en el Object() object, que es el más alto nivel padre. Si la propiedad aún no es encontrada, la propiedad será indefinida.

  Previamente sólo definimos métodos directamente en el constructor. Veamos cómo se definen en el prototipo.

  ```
  function Dog(age, weight, name) {
    this.age = age;
    this.weight = weight;
    this.name = name;
  }

  Dog.prototype.bark = function () {
      console.log(`${this.name} says woof!`);
  };

  dog1 = new Dog(2, 60, 'Java');
  dog1.bark(); // Java says woof!
  ```
  <br/>

  #### 3.5.3. Question

  ```
  // (A)
  function Dalmatian (name) {
    this.name = name;
    this.bark = function() {
      console.log(`${this.name} barks!`);
    };
  }

  // (B)
  function Dalmatian (name) {
    this.name = name;
  }
  Dalmatian.prototype.bark = function() {
    console.log(`${this.name} barks!`);
  };
  ```
  <br/>

  Let s say that we want to define a method that can be invoked on instances (objects) of the Dalmatian constructor function (we ll be instantiating at least 101 of them!). Which of the preceding two approaches is optimal? (B) is optimal, because the function that bark points to does not need to be recreated each time an instance of Dalmatian is created.

  While both approaches work just fine (i.e., any instances created by the constructor function will be able to invoke a bark() method), the second approach is more ideal. By adding methods to the prototype, memory is saved as more Dalmatian objects are instantiated. Along with being more efficient, we also don t have to update all objects individually should be decide to change a method.

  #### 3.5.4. Replacing the prototype Object
  Qué pasa si reemplazamos completamente la función prototípica de un objeto? Cómo afecta esto a los objetos creador por esa función?
  
  ```
  function Hamster() {
    this.hasFur = true;
  }

  let waffle = new Hamster();
  let pancake = new Hamster();

  Hamster.prototype.eat = function () {
    console.log('Chomp chomp chomp!');
  };

  waffle.eat();  // 'Chomp chomp chomp!'
  pancake.eat();  // 'Chomp chomp chomp!'
  ```
  <br/>

  Los objetos definidos anteriormente no tendrán acceso a lo que agreguemos a continuación.
  Sólo mantienen su lazo al viejo prototipo.

  ```
  Hamster.prototype = {
    isHungry: false,
    color: 'brown'
  };

  console.log(waffle.color); // undefined
  waffle.eat(); // 'Chomp chomp chomp!'
  console.log(pancake.isHungry); // undefined
  ```
  <br/>

  Sólo este objeto que crearemos a continuación tendrá acceso al prototipo actualizado.
  Y no tendrá acceso al viejo prototipo.

  ```
  const muffin = new Hamster();
  muffin.eat(); // TypeError: muffin.eat is not a function
  console.log(muffin.isHungry); // false
  console.log(muffin.color); // 'brown' 
  ```
  <br/> 

  #### 3.5.5. Video

  ```
  const myArray = [1, 2, 3];
  myArray.join(''); // 123
  console.dir(myArray);

  Retorna:
  ▼ Array(3)
    0: 1
    1: 2
    2: 3
    length: 3
    ▼ __proto__: Array(0)
      ▶ constructor: ƒ Array()
      ▶ etc.
  ```
  <br/>

  Enlista todos los métodos disponibles para llamar con nuestro array. Todos son prototípicos. Estos métodos no son definidos en el array o en el objeto, sino que el array individual tiene acceso a métodos heredados del prototipo.

  #### 3.5.6. Checking an Object s Properties
  Si un objeto no tiene una propiedad partircular en sí misma, puede acceder a alguna desde algún lugar de la cadena prototípica, asumiendo que exista. Con tantas opciones resulta tricky decir de donde proviene una propiedad particular. 

  Los siguientes métodos pueden resultar útiles para este tipo de casos:

  #### 3.5.7. hasOwnProperty()
  Nos permite encontrar el origen de una propiedad. Pasando el string de la propiedad que estamos buscando, el método retornará un boolean indicando si esa propiedad pertenece o no a ese objeto, es decir esa propiedad no es heredada. 

  ```
  function Phone() {
    this.operatingSystem = 'Android';
  }
  Phone.prototype.screenSize = 6;

  const myPhone = new Phone();
  const own = myPhone.hasOwnProperty('operatingSystem');
  console.log(own);  // true

  const inherited = myPhone.hasOwnProperty('screenSize');
  console.log(inherited); // false
  ```
  <br/>

  Nos devuelve verdadero sobre la propiedad que fue creada dentro del constructor, pero falso para la propiedad que pertenece al prototipo.

  #### 3.5.8. isPrototypeOf()
  Este método chequea si un objeto existe o no dentro de otra cadena de prototipos. Podemos confirmar si un objeto particular sirve como prototipo para otro objeto.

  ```
  const rodent = {
    favoriteFood: 'cheese',
    hasTail: true
  };  

  function Mouse() {
    this.favoriteFood = 'cheese';
  }

  Mouse.prototype = rodent;

  const ralph = new Mouse();
  const result = rodent.isPrototypeOf(ralph);
  console.log(result);  // true
  ```
  <br/>

  Para utilizar este método necesitamos saber el prototipo.

  #### 3.5.9. Object.getPrototypeOf()
  En el caso de que no estemos seguros de qué prototipo sea podemos utilizar este método. 

  ```
  const rodent = {
    favoriteFood: 'cheese',
    hasTail: true
  };  

  function Mouse() {
    this.favoriteFood = 'cheese';
  }

  Mouse.prototype = rodent;

  const ralph = new Mouse();
  const myPrototype = Object.getPrototypeOf(ralph);
  console.log(myPrototype); // { favoriteFood: 'cheese', hasTail: true }
  ```
  <br/>

  #### 3.5.10. The constructor Property
  Cada vez que un objeto es creado una propiedad especial es asignada por debajo: constructor. Accediendo a la propiedad del constructor del objeto podemos retornar una referencia de la función constructora que crea ese objeto en primer lugar. 

  ```
  function Longboard() {
    this.material = 'bamboo';
  }

  const board = new Longboard();

  console.log(board.constructor);
  // function Longboard() {
  //   this.material = 'bamboo';
  // }
  ```
  <br/>

  Recuerda que en el caso de que el objeto haya sido creado con notación literal el constructor será Object()

  ```
  const rodent = {
    favoriteFood: 'cheese',
    hasTail: true
  };

  console.log(rodent.constructor);  
  // function Object() { [native code] }
  ```
  <br/>

  #### 3.5.11. Question
  What is true about hasOwnProperty()? 
  - It returns a boolean indicating whether the object has the specified property as its own property (i.e., the property isn t inherited)
  - hasOwnProperty() is invoked as a method onto an object

  What is true about isPrototypeOf() or getPrototypeOf()? Select all that apply:
  - isPrototypeOf() checks whether or not an object exists in another object s prototype chain
  - isPrototypeOf() takes a single argument: an object whose prototype chain is to be searched
  - getPrototypeOf() returns the prototype of the object passed into It

  What is true about constructor property? Select all that apply:
  - Accessing an object s constructor property returns a reference to the constructor function that created that object (instance)
  - Every object has a constructor property
  - Objects created with literal notation are constructed with the Object() constructor function
  
  #### 3.5.12. Question
  Let's say that we create the following object, capitals, using regular object literal notation:

  ```
  const capitals = {
    California: 'Sacramento',
    Washington: 'Olympia',
    Oregon: 'Salem',
    Texas: 'Austin'
  };
  ```

  What is returned when Object.getPrototypeOf(capitals) is executed?
  A reference to Object()'s prototype

  This one may have been tricky! Keep in mind that since capitals was created with object literal notation, its constructor is the built-in Object() constructor function itself! As such, it maintains a reference to its constructor s prototype. That is,
  
  ```
  Object.getPrototypeOf(capitals) === Object.prototype; // true
  ```
  <br/>

  #### 3.5.13. Summary
  Herencia en JS es cuando un objeto se basa en otro objeto. La herencia nos permite reusar código existente, teniendo objetos tomamos propiedades de otros objetos.

  Cuando llamamos a una función usando el operador new la función crea y devuelve un nuevo objeto. Este objeto es secretamente enlazado al prototipo de su constructor, que es otro objeto. Usando este enlace secreto nos permite acceder a las propiedades y métodos del prototipo como si fueran propios. Si JS no encuentra una propiedad particular en un objeto, seguirá buscando en la cadena prototípica, eventualmente alcanzado Object() en el nivel top parent.

  También vimos los métodos:
  - hasOwnProperty()
  - isPrototypeOf()
  - Object.getPrototypeOf()
  - .constructor

  #### 3.5.14. Further Research
  - Object Playground: http://www.objectplayground.com/
  - hasOwnProperty() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty
  - isPrototypeOf() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isPrototypeOf
  - Object.getPrototypeOf() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf
  - .constructor on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor

  ### 3.6. Prototypal Inheritance: Subclases

  #### 3.6.1. Subclasses
  Uno de los beneficios de implementar herencia es que nos permite reutilizar código existente. Estableciendo herencias, podemos subclass, eso es tener un hijo objeto con la mayoría o todas las propiedades padre mientras mantiene propiedades únicas por sí mismo. Digamos que tenemos un objeto padre Animal, que contiene propiedades como edad y peso. El mismo animal puede acceder también a métodos como comer y dormir.
  Ahora, digamos también, que quisiéramos crear un hijo objeto Cat. Así como podemos hacer con otros animales, también podemos describir la edad o peso del gato, y también sabemos que puede también comer y dormir. 
  Cuando creamos un objeto Cat, entonces podemos simplemente re escribir y re implementar esos métodos y propiedades de Animal. O podemos ahorrar cierto tiempo y prevenir código repetido haciendo que Cat herede las existentes propiedades y métodos desde Animal. No sólo puede Car tomar las propiedades o métodos de Animal, sino también dar a Cat sus propiedades y métodos únicos. Tal vez Cat tenga un propiedad lives con un valor de 9 o tenga un método especial meow() que Animal no tiene.
  
  Utilizando herencia prototípica, Cat sólo necesita implementar funcionalidades específicas de Cat, y reutilizar las existentes funcionalidades ya en Animal.

  #### 3.6.2. Inheritance Via Prototypes
  Recordemos la cadena prototípica de la sección previa:

  ```
                          ╔═════════════════╗  ╔═════════════════╗  ╔═════════════════╗
                          ║   constructor   ║  ║   constructor   ║  ║   constructor   ║
  ╔═══════════════╗  new  ╠═════════════════╣  ╠═════════════════╣  ╠═════════════════╣
  ║    bailey     ║   ↵   ║       Cat()     ║  ║     Animal()    ║  ║     Object()    ║
  ╠═══════════════╣       ╚═════════════════╝  ╚═════════════════╝  ╚═════════════════╝ 
  ║    lives      ║                ┋                    ┋                    ┋           ╔═════════════════╗
  ╚═══════════════╝       ╔═════════════════╗  ╔═════════════════╗  ╔═════════════════╗  ║    undefined    ║    
          ╹               ║    prototype    ║  ║    prototype    ║  ║    prototype    ║  ╚═════════════════╝
          ╹               ╠═════════════════╣  ╠═════════════════╣  ╠═════════════════╣           ╹
          ┗╺╺╺╺╺╺╺╺╺╺╺╺╺╺ ║      meow()     ║╺╺║     kingdom     ║╺╺║ hasOwnProperty()║╺╺╺╺╺╺╺╺╺╺╺┛ 
                          ║                 ║  ║  calculateAge() ║  ║ isPrototypeOf() ║
                          ╚═════════════════╝  ╚═════════════════╝  ╚═════════════════╝ 

  ```
  <br/>
  
  Cuando llamamos cualquier propiedad en cualquier objeto, el motor JS primero busca la propiedad en el objeto mismo. Si la propiedad no es encontrada buscará en el prototipo del objeto. Si la propiedad aún no es encontrada JS seguirá buscando en la candena prototípica.

  Otra vez, herencia en JS es todo acerca de setear esta cadena.

  #### 3.6.3. The Secret Link
  La función constructora de un objeto es el primer lugar donde el motor de JS intenta acceder a una propiedad que no es encontrada en el objeto mismo. 

  ```
  const bear = {
    claws: true,
    diet: 'carnivore'
  }; // Nuevo objeto con dos propiedades

  function PolarBear() { 
    // ...
  }; // Creamos una función constructora

  PolarBear.prototype = bear; // Se la asignamos al prototipo de bear

  const snowball = new PolarBear(); // Creamos una instancia para el nuevo objeto

  snowball.color = 'white'; 
  snowball.favoriteDrink = 'cola'; // Y le asignamos dos propiedades
  
  {
    color: 'white',
    favoriteDrink: 'cola'
  }; // El objeto hasta ahora se ve así

  console.log(snowball.claws); // true 
  console.log(snowball.diet); // 'carnivore' - También a las propiedades de bear
  ```
  <br/>

  Ambas propiedades existen en el prototipo del objeto, y son alcanzadas por este enlace secreto que tienen con las propiedades de la función constructora del prototipo.

  Qué es este enlace secreto que hace referencia hacia el objeto prototipo? Justo después de que los objetos son creados desde el constructor PolarBear(), tienen acceso inmediato a las propiedades en el prototipo PolarBear(). Pero cómo es posible?

  La propiedad __proto__ de snowball es una propiedad de todos los objetos, hechos por una función constructora, y apunta directamente a la constructora del prototipo del objeto. 

  ```
  console.log(snowball.__proto__); // { claws: true, diet: 'carnivore' }
  ```
  <br/>

  Como la propiedad __proto__ refiere al mismo objeto como el prototipo de PolarBear, bear al compararlos retorna true:

  ```
  console.log(snowball.__proto__ === bear); // true
  ```
  <br/>

  Es altamente DESACONSEJABLE reasignar el objeto __proto__ o utilizarlo en cualquier código que escribas. Primero, hay problemas de compatibilidad cross-browser. Como el motor JS busca y accede a propiedades a lo largo de la cadena prototípica, mutar la propiedad
  de un objeto puede llevar a problemas de performance. Tampoco debe utilzarse para manejar herencia. Si alguna vez sólo necesitas rever el prototipo de un objeto todavía puedes utilizar Object.getPrototypeOf().

  #### 3.6.4. What About Just Inheriting the Prototype?
  Digamos que queremos que Child herede desde Parent. Por qué no deberíamos setear Child.prototype = Parent.prototype ?

  Primero, recordemos que los objetos son pasados por referencia. Esto quiere decir que Child.prototype y Parent.prototype refieren al mismo objeto, cualquier cambio realizado en Child se hará también en Parent. No queremos que que los hijos sean capaces de modificar las propiedades de sus padres.

  Encima de todo esto, ninguna cadena prototípica será seteada. Qué pasa si queremos que un objeto herede de cualquier objeto que querramos y no sólo su prototipo? Necesitamos un manejo aún más eficiente de las herencias sin mutar el prototipo para nada.

  #### 3.6.5. Question
  
  ```
  function GuineaPig (name) {
    this.name = name;
    this.isCute = true;
  }

  const waffle = new GuineaPig('Waffle');

  What does waffle.__proto__ refer to?
  GuineaPig.prototype
  ```
  <br/>

  #### 3.6.6. Question

  ```
  function Car (color, year) {
    this.color = color;
    this.year = year;
  }

  Car.prototype.drive = function () {
    console.log('Vroom vroom!');
  };

  const car = new Car('silver', 1988);
  ```
  <br/>

  What happens when car.drive() is executed? List the following events in the order that they occur:
  - Primero, el motor JS busca dentro del objeto car por una propiedad llamada drive
  - El motor JS no encuentra la propiedad drive dentro del objeto car
  - El motor JS entonces accede a la propiedad car.__proto__
  - Como la propiedad car.__proto__ apunta a Car.prototype, el motor JS busca drive en el prototipo
  - Como Car.prototype.drive es una función definida, es retornada
  - Finalmente, como drive es invocado como un método en car, el valor de this es seteado a car

  #### 3.6.7. Object.create()
  Recordar: aunque podamos acceder al prototipo a través de __proto__, no es una buena práctica. No deberíamos utilizar la herencia desde el prototipo. Esto no permite que se setee la cadena prototípica y cualquier cambio realizado en el objeto hijo se verá reflejado en el objeto padre.

  Pero hay una forma de setear el prototipo de un objeto nosotros mismos: usando Object.create(). Y lo mejor de todo, es que este approach nos permite manejar la herencia sin alterar el prototipo.

  Object.create() toma un simple objeto como argumento, y retorna un nuevo objeto que es la propiedad __proto__ seteada con el argumento pasado dentro de ella. Desde este punto, simplemente seteamos el objeto retornado para ser la función construnctora del prototipo del objeto hijo.

  ```
  const mammal = {
    vertebrate: true,
    earBones: 3
  }; // Seteamos el objeto mammal con dos propiedades

  const rabbit = Object.create(mammal); // El objeto retornado seteará __proto__ del objeto pasado como arg

  console.log(rabbit); // {} - Esperamos que el objeto esté vacío sin propiedades

  console.log(rabbit.__proto__ === mammal); // true - rabbit está enlazado a mammal.

  console.log(rabbit.vertebrate); // true
  console.log(rabbit.earBones); // 3
  ```
  <br/>

  Esto quiere decir que rabbit se extiende de mammal. Como resultado rabbit puede acceder a las propiedades de mammal.

  Object.create() nos da un método limpio para establecer herencia prototípica en JS. Podemos fácilmente extender la cadena prototípica de esta manera y podemos tener objetos heredados desde cualquier objeto que querramos.

  ```
  function Animal (name) {
    this.name = name;
  }

  Animal.prototype.walk = function () {
    console.log(`${this.name} walks!`);
  };

  function Cat (name) {
    Animal.call(this, name); // Llamamos al superconstructor para la instancia cat u objetos cat, sino this.name será undefined
    this.lives = 9;
  }

  Cat.prototype = Object.create(Animal.prototype); // Hacemos que Cat herede de Animal

  Cat.prototype.constructor = Cat; // Cambiamos el constructor, sino todos los Cat apuntarán a Animal

  Cat.prototype.meow = function () {
    console.log('Meow!'); // Creamos un método
  };

  const bambi = new Cat('Bambi'); // Creamos un objeto Cat

  bambi.meow(); // Meow! 
  bambi.walk(); // Bambi walks!
  bambi.name; // Bambi
  ```
  <br/>

  #### 3.6.8. Question
  Consider the following:

  ```
  function Parent() {
    // ...
  }

  function Child() {
    // ...
  }

  Child.prototype = Object.create(Parent.prototype);
  const child = new Child();

  // The following is then executed: 
  child instanceof Parent;

  // What is printed to the console? 
  true
  ```
  <br/>

  #### 3.6.9. Question
  What is true about Object.create()?
  - It returns a new object whose __proto__ property is set to the object passed into Object.create()
  - Using Object.create(), we can have objects inherit from just about any object we want (i.e., not only the prototype)
  - Object.create() allows us to implement prototypal inheritance without mutating the prototype

  #### 3.6.10. Summary
  Herencia en JS es sobre setear la cadena prototípica. Esto permite subclasear, crear hijos objeto que hereden la mayoría o todas las propiedades y métodos padre. Podemos entonces implementar cualquier propiedad o herencia particular al hijo de manera separada, mientras mantenemos data y funcionalidades de sus padres.

  Un objeto o instancia, está secretamente linkeado al objeto prototipo de su función constructora a través de la propiedad __proto__. No debemos utilizar __proto__ en nuestro código, esto  llevaría a efectos no deseados.

  Para manejar la herencia de manera efectiva en JS y para evitar mutaciones del prototipo existe Object.create() que nos permite justamente hacer eso, tomar un objeto padre y retornar un nuevo objeto con su propiedad __proto__ seteada por el objeto padre.

  #### 3.6.11. Further Research
  - Inheritance and the prototype chain on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
  - Object.create() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create
  
  ### 3.7. Lesson Summary

  ### 3.8. Course Outro