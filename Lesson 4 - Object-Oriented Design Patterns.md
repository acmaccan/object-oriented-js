  # Object-Oriented JavaScript

  ## 4. Object-Oriented Design Patterns
  
  ### 4.1. Introduction
  - Mixins
  - Module Pattern
  - Revealing Module Pattern

  ### 4.2. Mixins / Extending Object Functionality with Mixins
  
  #### 4.2.1. An Object is Prototype-linked to a Single Object
  Recordemos que la propiedad .prototype de un objeto apunta sólo a UN objeto. Esto es porque JS soporta herencia simple. Si hay un objeto A y un objeto B, objeto C puede solor recibir de A o B. El objeto cat está linkeado al prototipo de un sólo objeto: animal.

                    ╔═════════════════════════╗     ╔══════════════╗
                    ║         animal          ║     ║     cat      ║
                    ║  {                      ║     ║  {           ║
                    ║    kingdom: 'Animalia'  ║╺╺╺╺╺║    lives: 9  ║
                    ║  }                      ║     ║  }           ║
                    ╚═════════════════════════╝     ╚══════════════╝

  #### 4.2.2. Question
  What is true about the following?

  ```
  const aircraft = {
    flies: true
  };

  const helicopter = Object.create(aircraft);
  console.log(helicopter.flies); 
  // true
  ```
  <br/>

  - The helicopter object has no properties of its own
  - helicopter is prototype-linked to aircraft

  #### 4.2.3.Mixins
  Si un objeto JS sólo puede ser prototípicamente enlazado a un objeto, cómo podríamos extender propiedades y métodos de múltiples fuentes? Podemos hacelo con mixins. 
  Mixin es una técnica que permite tomar las propiedades y métodos de un objeto, y copiarlas en otro objeto. De esta forma generamos objetos con nuevas funcionalidades sin involucrar herencias y que no
  pertenecen a la cadena prototípica del objeto.

  #### 4.2.4. Object.assign()
  La manera más sencilla de implementar mixin patterns es usando Object.assign(), un método que copia las propiedades de uno o más objetos source dentro de un objeto target. Luego retorna ese objeto target actualizado.

  ```
  let target = {};
  let source = { number: 7 };
  Object.assign(target, source);

  console.log(target); 
  // { number: 7 }
  ```
  <br/>

  El primer argumento pasado en target, es el destino que va a recibir las propiedades copiadas del objeto source. Notemos que Object.assign() no crea y retorna un nuevo objeto. Directamente modifica y luego retorna el mismo objeto target que fue pasado dentro. Entonces, los valores existentes serán sobreescrito, mientras que las propiedades que no existan en el objeto source permanecerán intactas.

  ```
  let target = { letter: 'a', number: 11 };
  let source = { number: 7 };
  Object.assign(target, source);

  console.log(target); 
  // { letter: 'a', number: 7 }
  ```
  <br/>

  #### 4.2.5. Multiple Source Objects
  Object.assign() puede tomar diferentes objetos source. 

  ```
  const duck = {
    hasBill: true,
    feet: 'orange'
  };
  const beaver = {
    hasTail: true
  };
  const otter = {
    hasFur: true,
    feet: 'webbed'
  };

  const platypus = Object.assign({}, duck, beaver, otter);

  console.log(platypus); 
  // { hasBill: true, hasTail: true, hasFur: true, feet: 'webbed' }
  ```
  <br/>

  Luego de mergear un objeto vacío con las propiedades de duck, beaver y otter el objeto target es retornado con todas, las cuatro propiedades. Es importante notar que platypus no está linkeado con el prototipo de los otros tres objetos, platypus no existe en la cadena prototípica de los tres objetos y viceversa.

  ```
  platypus.constructor; // Object()
  platypus.isPrototypeOf(duck); // false
  duck.isPrototypeOf(platypus); // false
  platypus.isPrototypeOf(beaver); // false
  beaver.isPrototypeOf(duck); // false
  platypus.isPrototypeOf(otter); // false
  otter.isPrototypeOf(platypus); // false
  ```
  <br/>

  #### 4.2.6. Object.assign() Compatibility
  Object.assign() fue introducido a la especificación ES2015 (ES6), por lo que puede presentar problemas de compatibilidad: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign#Browser_compatibility

  #### 4.2.7. Question
  Let's modify the above code a bit. 

  ```
  const duck = {
    hasBill: true
  };
  const beaver = {
    hasTail: true
  };
  const otter = {
    hasFur: true,
    feet: 'webbed'
  };

  const platypus = Object.assign(duck, beaver, otter);
  ```
  <br/>

  What is true after the following?
  - platypus is an object with four properties
  - duck becomes an object with four properties
  - platypus === duck

  #### 4.2.8. Question
  What is true about multiple inheritance or mixins?
  - A mixin supplies properties and/or methods that can be shared
  - We can leverage Object.assign() to "mix in" properties and methods from a number of objects
    into a composite object

  #### 4.2.9. Summary
  El mixin es una técnica que copia data y funcionalidades desde un/os objeto/s source a un objeto target. Podemos implementarlo a través del método Objeto.assign() (ES6) para retornar un objeto target con propiedades de uno o más objetos mezclados dentro del objeto target.
  
  #### 4.2.10. Further Research
  - Object.assign() on MDN: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign

  ### 4.3. Functional mixins
  
  #### 4.3.1. Remember Constructor Functions?
  Previamente utilizamos una función constructora para crear nuevo objetos:

  ```
  function City(name, population) {
    this.name = name;
    this.population = population;

    this.identify = function () {
      console.log(`${this.name} s population is ${this.population}.`);
    };
  };
  ```
  <br/>

  Para instanciarlo, invocamos una función con el operador new:

  ```
  const sanFrancisco = new City('San Francisco', 870000);
  console.log(sanFrancisco);

  {
    name: 'San Francisco',
    population: 870000,
    identify: function () {
      console.log(`${this.name} s population is ${this.population}.`);
    };
  }
  ```
  <br/>

  Podemos utilizar el mismo constructor para crear múltiples objetos:

  ```
  const mountainView = new City('Mountain View', 78000);
  console.log(mountainView);
  {
    name: 'Mountain View',
    population: 78000,
    identify: function () {
      console.log(`${this.name} s population is ${this.population}.`);
    };
  }
  ```
  <br/>

  Notemos como utilizamos el operador new para la creación de cada uno de los objetos, cada vez. Las factory functions producen instancias de objeto sin el uso del operador new.

  #### 4.3.2. Factory Functions
  Son funciones que retornan un objeto, pero en sí mismas no son una clase o un constructor. Invocamos una factory function como una función normal sin utilizar el operador new. Con ella podemos crear fácilmente instancias de objetos sin la complejidad de clases y constructores.

  ```
  function Basketball(color) {
    return {
      color: color,
      numDots: 35000
    };
  };
  ```
  <br/>

  Lo que es importante para notar aquí es que Basketball() retorna un objeto directamente. Es diferente de una constructor function que retorna su objeto automáticamente.

  ```
  const orangeBasketball = Basketball('orange');
  console.log(orangeBasketball); 
  // { color: 'orange', numDots: 35000 }
  ```
  <br/>

  Una factory function tiene su nombre, tal como una fábrica de sillas puede producir silla después de silla, una factory function puede ser usada una y otra vez para crear n objetos.

  ```
  const myBB = Basketball('blue and green');
  const yourBB = Basketball('purple');
  const bouncy = Basketball('neon pink');
  ```
  <br/>

  Invocando la factory function nos permite componer un simple objeto, sin el uso del operador new. Sumaricemos las diferencias entre factory function y constructor function.

  ```
  ╔════════════════════════════════════╦════════════════════════════╦════════════════════════════╗
  ║                                    ║ Factory Function           ║ Constructor Function       ║
  ╠════════════════════════════════════╬════════════════════════════╬════════════════════════════╣
  ║ Creates a new object?              ║ Yes                        ║ Yes                        ║     
  ╠════════════════════════════════════╬════════════════════════════╬════════════════════════════╣
  ║ Can be called multiple times       ║ Yes                        ║ Yes                        ║ 
  ║ to create multiple objects?        ║                            ║                            ║       
  ╠════════════════════════════════════╬════════════════════════════╬════════════════════════════╣
  ║ Can receive arguments?             ║ Yes                        ║ Yes                        ║     
  ╠════════════════════════════════════╬════════════════════════════╬════════════════════════════╣
  ║ Implicates prototypal inheritance? ║ No                         ║ Yes                        ║  
  ╠════════════════════════════════════╬════════════════════════════╬════════════════════════════╣
  ║ Invoked as...                      ║ A normal function          ║ With the new operator      ║
  ║                                    ║ factoryFunc()              ║ new constructorFunc()      ║
  ╚════════════════════════════════════╩════════════════════════════╩════════════════════════════╝ 
  ```
  <br/>

  #### 4.3.3. Video
  Esta es una factory function que retorna un closure. Como la instancia de una clase, el closure tiene sus propias functiones y variables. 
  Tanto turnOn como isOn hacen referencia a la variable on declarada dentro de Radio. Lo que este objeto está haciendo es cerrar sobre una variable definida sobre la función padre. De esta forma, preserva su estado.

  ```
  function Radio(mode) {
    let on = false;

    return {
      mode: mode,
      turnOn: function () {
        on = true;
      },
      isOn: function () {
        return on;
      }
    };
  }

  let fmRadio = Radio('fm'); // Inovcamos la función y le asignamos fm a mode
  fmRadio.on; //undefined - No podemos acceder

  fmRadio; // Si miramos la estructura, on en sí mismo no es una propiedad del objeto fmRadio
    ▶ { mode: "fm", turnOn: ƒ, isOn: ƒ }

  fmRadio.isOn(); // false - Este método isOn hace referencia a on, podemos acceder a él a través de isOn
  fmRadio.turnOn(); // Llamamos a este método
  fmRadio.isOn(); // true - Reasignó el valor de on
  ```
  <br/>

  Entonces, podemos aprovechar factory functions junto con closures para preservar estados.

  #### 4.3.4. Functional Mixins
  Entonces, utilizamos mixins para agregar features a un objeto compuesto. También aprovechamos factory functions para crear objetos sin el operador new o sin utilizar le herencia prototípica. Combinando todo esto podemos dar un paso más allá con functional mixins.

  Un functional mixin es una factory function componible que recibe una mixin como argumento, copia propiedades y métodos desde esa mixin y retorna un nuevo objeto. 

  ```
  function CoffeeMaker(object) {
    let needsRefill = false;

    return Object.assign({}, object, {
      pourAll: function () {
        needsRefill = true;
      },
      isEmpty: function () {
        return needsRefill;
      }
    });
  }
  ```
  <br/>

  Notemos que a diferencia de una factory function standard, que toma valores individuales de una propiedad, la functional mixin en realidad toma un objeto en sí mismo. Cual sea el objeto pasado en la función es mergeado con otros objetos pasados en Object.assign()

  ```
  const mixedCoffeeMaker = CoffeeMaker({ style: 'percolator' });

  // El objeto mixedCoffeeMaker retornado:
  {
    style: 'percolator',
    pourAll: function () {
      needsRefill = true;
    },
    isEmpty: function () {
      return needsRefill;
    }
  }
  ```

  Functional mixins son componibles. Podemos utilizar piezar individuales de código para agregar propiedades específicas como una línea de ensamble. 

  ```
  function IceCreamFactory(obj) {  → Toma un sólo objeto, tiene una variable local y retorna el valor de Object.assign
    let isCold = true;

        Objeto target vacío    Objeto source, el argumento de IceCreamFactory
                          ↑    ↑
    return Object.assign({}, obj, {   → dos métodos: melt e isCold
      melt: function () {
        isCold = false                → Cambia el valor de isCold
      },
      isCold: function () {
        return isCold                 → Trae el valor de isCold
      }
    });
  }

  let iceCream = IceCreamFactory({}); // Guardamos la functional mixin en una variable

  iceCream; // Si vemos la estructura
    ▶ { melt: ƒ, isCold: ƒ }

  function ConeFactory(obj) {  → Creamos otra, repitiendo la estructura anterior
    let isDry = true;

    return Object.assign({}, obj, {
      soggy: function () {
        isDry = false;
      },
      isDry: function () {
        return isDry;
      }
    });
  }
                                                  Objeto vacío
                                                  ↑
  let iceCreamCone = IceCreamFactory(ConeFactory({})); // Retornamos el valor de coneFactory como argumento de IceCreamFactory

  iceCreamCone; // Si vemos la estructura
    ▶ { soggy: ƒ, isDry: ƒ, melt: ƒ, isCold: ƒ }

  console.log(iceCreamCone);
  ```
  <br/>

  #### 4.3.5. Question
  What is true about factory functions or mixins?
  - Just like a constructor function, a factory function can be called multiple times to create an object

  ### 4.3.6. Summary
  Una factory function crea objetos. Es invocada como una función normal sin el operador new. Con functional mixims podemos ir un poco más allá, aceptando un mixin como argumento, copia propiedades y métodos del mixin y retorna un nuevo objeto.
  
  ### 4.3.7. Further Research
  - JavaScript Factory Functions vs Constructor Functions vs Classes by Eric Elliott: https://medium.com/javascript-scene/javascript-factory-functions-vs-constructor-functions-vs-classes-2f22ceddf33e
  - Factory Function Pattern In-Depth by Ronald Chen: https://medium.com/@pyrolistical/factory-functions-pattern-in-depth-356d14801c91

  ### 4.4. Module Pattern
  
  #### 4.4.1. Private Properties: Literal
  Por defecto, la mayoría de las cosas en JS son accesibles. Podemos utilizar closure para hacer ciertas partes del código privadas. Pero qué pasa si queremos prevenir el acceso de manera directa? Cómo podemos hacer que una propiedad o método sea privada e inaccesible desde fuera? 

  ```
  let developer = {
    name: 'Veronika',
    getName: function () {
      return this.name;
    }
  };

  // Podemos acceder a 'Veronika' a través de getName o de name:
  developer.getName(); // 'Veronika'
  developer.name; // 'Veronika'

  //Qué pasa si reasignamos el valor de nombre?
  developer.name = 'Not Veronika';

  developer.getName(); // 'Not Veronika'
  developer.name; // 'Not Veronika'
  ```
  <br/>

  #### 4.4.2. Privacy with Underscores?
  Los guiones bajos que podemos llegar a ver en código son sólo convención entre desarrolladores para indicar una variable privada, pero no tiene funcionalidad.

  #### 4.4.3. Private Properties: Function
  Qué pasa si creamos una función básica que sólo retorne un objeto? Da esto el nivel adecuado de protección?

  ```
  function instantiateDeveloper() {
    return {
      name: 'Veronika',
      getName: function () {
        return this.name;
      }
    };
  }; // Función básica que retorna un objeto con dos propiedades: name y getName.

  let developer = instantiateDeveloper(); // Invoquemos la función para obtener el objeto

  El nombre todavía es accesible:
  developer.getName; // 'Veronika'
  developer.name; // 'Veronika'

  Lo que todavía hace posible mutar el objeto:
  developer.name = 'Not Veronika';
  developer.name; // 'Not Veronika'
  ```
  <br/>

  #### 4.4.4. La funciones no puede proteger a los objetos de la mutabilidad.

  #### 4.4.4.1. No Private Properties
  Como JS no tiene un concepto de propiedades privadas, no hay sintaxis especial o palabras clave que podamos utilizar para proteger ciertas propiedades de ser accedidas.

  Sin embargo, recordemos que aún podemos hacer uso de scopes y closures para crear un estado privado.
  ```
  function myCounter() {
    let count = 0;

    return function () {
      count += 1;
      return count; → Se cierra sobre la variables count
    }; 
  }

  let counter = myCounter();
  counter(); // 1
  counter(); // 2
  ```
  <br/>

  No hay método fuera del closure que nos permita acceder a count:
  ```
  counter.count; // undefined
  count; // undefined
  ```
  <br/>

  Entonces, closure nos provee una forma de crear data privada. Podemos sacar provecho de esta técnicas, scope y closure, para crear propiedades y métodos privados en un objeto?

  #### 4.4.5. Video
  En vez de utilizar un objeto literal o una simple función para crear privacidad podemos utilizar una unidad de organización un poco más grande llamada módulo, para alcanzar verdadera privacidad. Ésta se ha vuelto una técnica común y es conocida como module pattern. Este patrón utilza scope y closures para proteger las variables del acceso externo.
  
  #### 4.4.6. Question
  Before we jump into how the Module Pattern leverages scope and closures, let s make sure we re on the same page regarding scope. Consider the following:

  ```
  const myName = 'Richard';

  function introduceMyself() {
    const you = 'student';

    function introduce(message) {
      // Which variables can be used here?
    }

    return introduce('Hello');
  }
  ```
  <br/>

  Which variables does the nested introduce() function have access to?
  - myName - global
  - you - local
  - message - argument

  #### 4.4.7. Question
  Consider the following:

  ```
  let sodiumChloride = (function(){
    let chemicalFormula = 'NaCl';
    let molarMass = 58.44;

    return {
      getProperties: function(){
        console.log(`Formula: ${chemicalFormula}`);
        console.log(`Molar Mass: ${molarMass} g/mol`);
      }
    };
  })();
  ```
  <br/>

  When sodiumChloride.getProperties() is executed, what is logged to the console?
  - Two strings: 'Formula: NaCl' and 'Molar Mass: 58.44 g/mol'

  Recall that IIFEs are great for creating private state. That is, by wrapping chemicalformula and molarmass in an immediately-invoked function expression, those variables are inaccessible from the outside world.

  Module Pattern utiliza los funcionalidades de scope, closures e IIFEs para crear estados privados.

  ```
                Función inmediatamente invocada
                ↑
  let person = (function () {
    let name = 'Veronika'; → Variable local

    return  {
      getName: function () {
        return name; → getter
      },
      setName: function (myName){
        name = myName; → setter
      }
    };
  })(); → Paréntesis de invocación

  person.name; // undefined - Porque no está definido como propiedad en el objeto person
  person.getName; // 'Veronika' - Pero podemos acceder a través de este método
  person.setName('Not Veronika'); // Y podemos aún setear el valor de name a través de este método
  person.getName; // 'Not Veronika' - Comprobamos que name se ha modificado
  ```
  <br/>

  Y de esta forma podemos mantener un acceso privado a nuestros objetos, si no es a través de funciones definidas por nosotros mismos. Recordemos que JS no tiene funcionalidad de privacidad por default.

  #### 4.4.8. The Module Pattern: Recap
  
  ```
  let diana = (function () {
    let secretIdentity = 'Diana Prince';

    return {
      introduce: function () {
        console.log(`Hi! I am ${secretIdentity}`);
      }
    };
  })();
  ```
  <br/>

  Recordemos que el uso de IIFEs no sólo previene la polución global a través del scope sino que previene de accesos indeseados a ciertas variables. 
  ```
  console.log(diana.secretIdentity); 
  // undefined
  ```
  <br/>

  Y porque el objeto retornado de introduce() retiene el acceso al scope de las funciones padres, podemos dar una interfaz pública para interactuar con secretIdentity(); 
  ```
  diana.introduce(); // 'Hi! I am Diana Prince'
  ```
  <br/>
  
  #### 4.4.9. Other Benefits of the Module Pattern
  Hay otros beneficios más allá de la privacidad, al incorporar el module pattern. 
  - Organización: los módulos son grandes unidades de organización para funciones y objetos. Esto ayuda a particionar el código y proveer una estructura mientras la applicación escala.
  - Utilizamos module pattern cuando queremos sólo una verión de un objeto. Si estamos buscando instanciar objetos que sigan una cierta blueprint, siempre podemos escribir e invocar una función constructora.

  #### 4.4.10. Question
  What is true about the Module Pattern?
  - The Module Pattern uses closures to create private properties
  - The Module Pattern requires the use of IIFEs
  - Unlike calling a constructor function, implementing the Module Pattern returns just one version of an object

  #### 4.4.11. Summary
  Como JS no tiene variables, propiedades o métodos privados, podemos utilizar el module pattern
  para forzar la privacidad. En su core utiliza scopes, closures e IIFEs no sólo para esconder 
  data desde el acceso externo sino para proveer de una interfaz pública con esa data.

  #### 4.4.12. Further Research
  - Addy Osmani s The Module Pattern (JavaScript Design Patterns): https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript
  - Todd Motto s Mastering the Module Pattern: https://toddmotto.com/mastering-the-module-pattern/#private-methods 

  ### 4.5. The Revealing Module Pattern
  
  #### 4.5.1. Video
  Este patrón es muy similar al anterior, la filosofía debajo es la misma. La utilizamos para mantener la encapsulación. Pero en este patrón toda la data es privada y sólo la que el desarrollador considere es revelada públicamente.

  ```
                  IIFE
                  ↑
  let myModule = (function (){
    function privateMethod (message) { 
      console.log(message); → Creamos un método privado
    }

    function publicMethod (message) {
      privateMethod(message); → Creamos un método público
    }

    return {
      publicMethod: publicMethod  
    };  → Retornamos un objeto con una función pública
  })(); → Paréntesis para inmediatamente invocar a la función

  myModule; // Si vemos la estructura
    ▶ { publicMethod ƒ }

  myModule.publicMethod('hello there');
  // hello there
  ```
  <br/>

  #### 4.5.2. The Revealing Module Pattern
  La filosofía subyacente del Revealing Module Pattern es esa, mientras todavía mantenemos la encapsulación (como en el Module Pattern), también podemos revelar ciertas propiedades y métodos. Los ingredientes clave del Revealing Module Pattern:
  - Una IIFE (wrapper)
  - El contenido del módulo (variables, métodos, objetos, etc)
  - El retorno de un objeto literal

  #### 4.5.3. Another Example

  ```
  let person = (function () {
    let privateAge = 0;          → Data privada
    let privateName = 'Andrew';  → Data privada

    function privateAgeOneYear() { 
      privateAge += 1;           → Data privada
      console.log(`One year has passed! Current age is ${privateAge}`);
    }

    function displayName() {
      console.log(`Name: ${privateName}`);
    }

    function ageOneYear() {
      privateAgeOneYear();
    }

    return {   
      name: displayName,
      age: ageOneYear
    };  → El objeto retornado nos provee de una interfaz pública para acceder a la información
  })();
  ```
  <br/>

  person se ve:
  ```
  {
    name: displayName,
    age: ageOneYear
  };
  ```
  <br/>

  name revela la función privada displayName()
  ```
  console.log(person.name()); 
  // 'My name is Andrew'
  ```
  <br/>

  Qué pasa si intentamos acceder a ese método y mutarlo?
  ```
  person.privateName = 'Richard'; → Está intentando accede a privateName porque sólo existe en la IIFE misma
  console.log(person.name()); // 'My name is Andrew'
  ```
  <br/>

  Notemos que tampoco será efectivo accediendo a displayName()
  ```
  console.log(person.displayName()); 
  // undefined
  ```
  <br/>

  De la misma manera el Revealing Module Pattern también nos brinda a cceso a la variable privateAge vía el método del objeto retornado:
  ```
  console.log(person.age()); // 'One year has passed! Current age is 1'
  console.log(person.age()); // ''One year has passed! Current age is 2'
  ```
  <br/>

  #### 4.5.4. Question
  Which concepts make up the Revealing Module Pattern?
  - IIFE
  - Local variables/functions
  - Returned object literal with keys that point to data intended to be revealed

  #### 4.5.5. Benefits of the Revealing Module Pattern
  Cuando escribimos módulos, contamos con algunas ventajas usando este patrón.

  - Mayor claridad: al final del módulo, en el return statement, donde encontramos las variables y métodos que pueden ser accedidos públicamente. Los módulos pueden crecer y facilita la lectura para otros desarrolladores que lean tu código.
  
  - Sintaxis consistente. En contraste el Module Pattern normal, puede contenter variables y funciones repartidas por todo el cuerpo de la función.

  Nada puede salir mal con ninguno de los dos approaches para crear data privada, pero es importante dedicar tiempo a pensar cuál tiene mayor sentido para nuestro proyecto.

  #### 4.5.6. Summary
  El Revealing Module Pattern es una ligera variación del Module Pattern. IIFEs, variables y funciones locales, y el retorno de un objeto literal con data revelada hace a la estructura y sintaxis de este patrón. Mientras se mantiene la encapsulación de la data, ciertas variables y funciones son retornadas en un objeto literal.

  #### 4.5.7. Further Research
  - Addy Osmani's The Revealing Module Pattern (JavaScript Design Patterns): https://addyosmani.com/resources/essentialjsdesignpatterns/book/#revealingmodulepatternjavascript
  - Christian Heilmann s Again with the Module Pattern – reveal something to the world: https://christianheilmann.com/2007/08/22/again-with-the-module-pattern-reveal-something-to-the-world/

  ### 4.6. Lesson Summary

  ### 4.7. Course Outro
  - Objects: create, access and modify objects
  - Functions at runtime
  - Scopes, closures, IIFEs
  - Combinamos all to create our oun classes
  - Constructor functions
  - this keyword
  - Prototype inheritance to create and extend objects
  - Object-oriented Design Patterns: create, extend and add privacy to object.