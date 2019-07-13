# essentialConcepts

   // 1. Coercion
   // == or ===
   
   /*var a = 1
   var b = '1'
   a == b // true
   a === b // false, includes the type. a is a number, b is a string, therfore not identical
   // 2. Scope
    // Where identifiers, variables and functions are accessible
    // JS uses Function Scope
    // ES6 introduces block scope e.g let
    // Scope is a set of rules that determines where in a program you can access referenced items
        // Scope is determined lexically or by how you write the program
        // Everything starts in global scope but as things are made other scopes are created
        // Nested functions create scope chains
        // EXAMPLE 1
        var a = 10;
        var add5 = function(num) { // (*1.2)
            var b = 5;
            console.log(num + b); // (*1.3) 3 + 5 = 8
            var add10 = function(num2) { // (*2.2)
                console.log(num2 + a); // (*2.3) 3 + 10 = 13
            };
            add10(3); // (*2.1) 3 refers to num2
            var add15 = function(num3){ // (*3.2)
                var c = 15;
                console.log(num3 + c); // (*3.3) 3 + 15 = 18
            };
            add15(3); // (*3.1) 3 refers to num 3 and executes whole stack
        };
        // EXAMPLE 2
        var a = 10;
        var add5 = function(num) { // (*1.2)
            var b = 5;
            console.log(num + b); // (*1.3) 3 + 5 = 8
            var add10 = function(num2) { // (*2.2)
                console.log(num2 + c); // (*2.3) error, c is not in add10 scope.
                                      
            };
            add10(3); // (*2.1) 3 refers to num2
            var add15 = function(num3){ // (*3.2)
                var c = 15;
                console.log(num3 + c); // (*3.3) 3 + 15 = 18
            };
            add15(3); // (*3.1) 3 refers to num 3 and executes whole stack
        };
        // EXAMPLE 3
        var a = 10;
        var add5 = function(num) { // (*1.2)
            var b = 5;
            console.log(num + b); // (*1.3) 3 + 5 = 8
            var add10 = function(num2) { // (*2.2)
                console.log(num2 + a); // (*2.3) 3 + 10 = 13
                                      
            };
            add10(3); // (*2.1) 3 refers to num2
            var add15 = function(num3){ // (*3.2)
                var c = 15;
                add10(3) // (*3.3) 3 + 10 = 13
            };
            add15(3); // (*3.1) 3 refers to num 3 and executes whole stack
        };*/
   // 3, Nature of objects
    // Prototypal inheritance (see 8.)
        // Almost every object is linked to another object.
        // Linked object is called prototype.
        // The default object in JS does not have a prototype.
        // Objects inherit properties and methods from it's prototype ancestry.
            // Inherit means that object has access to higher object's properties and methods.
            // They are not a part of the object, but are part of the object's prototype.
            // Prototypes are automatically assigned to any object.
            // You can define an object's prototype.
        // EXAMPLE 1
/*
        var obj = {}; // There is nothing in the object, but it still has a prototype. e.g. toString is in the prototype and can be accessed.
        obj.toString = function() {console.log('Object')}; // This is now a part of the object.
        // EXAMPLE 2
        var arr = [1,2,3];
        arr.indexOf(2); // This returns 1 as indexOf is in the prototype.
        // How to set the prototype of an object:
        // Place reusable pieces in the prototype of an object
        // 3 most straight-forward methods
            // using a constructor function (see 7.)
            // using Object.create(prototype)
            // using Object.setPrototypeOf(obj, prototype) (this is ES6)
        // EXAMPLE 1 using a constructor function
        var objProto = {
            greet: function() {
                console.log(this.greeting + " World!");
            }
        };
        var Greeting = function(term) { // using uppercase 'G' to indicate constructor function
            this.greeting = term;
        };
        Greeting.prototype = objProto;
        var obj1 = new Greeting("Howdy"); // Type obj1.greet() into console displays: "Howdy World!"
        // This method is good for creating numerous objects of a similar type.
        // EXAMPLE 2 using Object.create(prototype)
        // This method is very straight-forward
        var obj2 = Object.create(objProto);
        obj2.greeting = "Hi"; // Type obj2.greet() into console displays: "Hi World!"
        // EXAMPLE 3 using Object.setPrototypeOf(obj, prototype)
        var obj3 = {
            greeting: "Hello"
        };
        Object.setPrototypeOf(obj3, objProto);
        // Type obj3.greet() into console displays: "Hello World!"
*/
   // 4. This
   // 'this' references the object that is executing the current function
   // If function is part of an object it is called a method 
   // method -> obj
   // If function is a regular function it references the global object (window)
   // function -> global(window)
/*
   const video = {
       title: 'a',
       play() {
           console.log(this);
       }
   };
   video.play();
*/
   // Becaused play is a method in the video object, this references the object itself
   // 5. Power of functions
    // Functions are objects in JS
    // Considered first class
    // Can be passed around and returned from other functions
    // Closures and IIFEs
   // 6. Namespace Pattern / Module Pattern
    // All serious development should take advantage of these patterns
   // 7. Constructor functions
   // Five important concepts
        // 1) Keyword 'new' is critical in a constructor
        // 2) Creates a new object, which is bound to 'this'.
        // 3) Function is invoked with the value of this equal to the new object.
        // 4) Sets the new object's prototype to the prototype property of the constructor.
        // 5) It returns the new object.
        // EXAMPLE 1
        /*
        function Users() { // uppercase 'U' indicates constructor
            console.log(this);
        };
        var user1 = Users();
        var user2 = new Users();
        // typing user1; returns undefined
        // typing user2; returns an Object as per concept 5).
        */
        
        // EXAMPLE 2
        /*
        function Users(fName, lName) { // uppercase 'U' indicates constructor
            this.firstName = fName;
            this.lastName = lName;
        };
        var user1 = Users("Matt", "Hey"); // still undefined as no keyword new
        var user2 = new Users("John", "Doe"); // constructs a new object with firstName 'John' and lastName 'Doe'
        */
        // EXAMPLE 3
/*
        function Users(fName, lName) { // uppercase 'U' indicates constructor
            this.firstName = fName;
            this.lastName = lName;
        };
        var user1 = new Users("Matt", "Hey");
        Users.prototype.fullName = function() {
            return this.firstName + ' ' + this.lastName
        };
        var user2 = new Users("John", "Doe");
        user1.fullName(); // returns "Matt Hey"
        user2.fullName(); // user2 has inherited the fullName function
*/
   // 8. Prototypal Inheritance
    // One object borrowing properties or methods from another object
    // An object can inherit from a parent object
    // Easier to think of as borrowing
    // EXAMPLE
/*
    var obj = {firstName: "Matt"};
    obj.toString(); // returns "[object Object]"
*/
