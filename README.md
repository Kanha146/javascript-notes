# javascript-notes


definition:
-----------
In JavaScript, a promise is an object that represents the eventual completion or failure of an asynchronous operation and its resulting value.

Promises are important because they allow us to write asynchronous code that is easier to read, write, and maintain. Instead of using nested callbacks or the "callback hell" pattern, we can chain promises together using methods like .then() and .catch() to handle success and error cases respectively.


1. What are Promises?
Promises are objects which are used to perform asynchronous operations. They are just like placeholders to store a future value that will be returned after some time. They contain two properties: PromiseState and PromiseResult.

 2. Importance of Promises:
a) Promises can help us to write trust worthy code.
b) Promises are used to solve the problems of callbacks like inversion of control and callback hell.
c) They give us the result prompt in three states: 1) Pending 2) Fulfilled 3) Rejected
d) We can attach function to promise object and retrieve its value unlike callbacks no need to pass the function.
e) Nesting can be done in Promises and with the help of that we can return the values in each individual chain.

Promises:-
-----------

1. Promise can be created using a new Promise() constructor function.
2. This constructor function takes a callback function as argument. 
3. The callback function has 2 arguments named 'resolve' and 'reject'. Resolve and reject are the keywords provided by JS.
4. We can only resolve or reject a promise. Nothing else can be done.
5. An error can also be created using new Error('error message').
6. There is also .catch() which is used to attach a failure callback function that handles any error that pops up during the execution of promise chain.
7. .catch only handles error of .then() that are present above it. If there is any .then() below it, catch will not handle any error for that, also that ,then will get executed no matter what.
8. It can be useful in a way if we want to catch error for a particular portion of a chain.
9. We can have multiple catch based on requirement and then a general catch at the end.
10. Always remember to return a value in the promise chain for the next .then to use .
11. If it returns a value => It will be  used as a parameter in next function. If it is a promise then the next .then in the promise chain is attached to the promise returned by the current callback function.

Homework:


     const cart = ['shoes', 'pants', 'kurta'];

     createOrder(cart)
    .then(function(orderId) {
    console.log(orderId);
    return orderId;
     })
    .then(function(orderID) {
    return proceedToPayment(orderID)
     })
    .then(function({ message, amt }) {
    console.log(message, 'of amount:', amt);
    return showOrderSummary(message, amt);
    })
    .then(function({ message, amt }) {
    console.log('Your wallet has beed debited by:', amt);
     })
    .catch(function(err) {
    console.log(err.message);
    })
     .then(function() {
       console.log('No matter what happens, I will get executed');
    });



    function createOrder(cart) {
    const pr = new Promise(function(resolve, reject) {
    // create order
    // Validate Cart
    // orderId
    if (!validateCart(cart)) {
      const err = new Error('Cart is not valid!');
      reject(err);
    }
    // logic for createOrder
    const orderId = '12345';
    if (orderId) {
      setTimeout(function() {
        resolve(orderId);
      }, 5000)
    }
    });

    return pr;
    }

    function proceedToPayment(orderID) {
     // Logic for handling payment.
    // This function returns a promise
    return new Promise(function(resolve, reject) {
    // logic
    resolve({ message: `Payment Successful for order id: ${orderID}`, amt: 2500 });
    })
    }

    function showOrderSummary(paymentInfo, amt) {
     return new Promise(function(resolve, reject) {
    // console.log(amt);
    if (amt >= 2000) {
      resolve({ message: 'You have ordered items that cost ${amt} RS', amt });
    } else {
      reject(new Error('Please buy more for discount'));
    }
    })
     }

    function validateCart(cart) {
     // code to validate cart.
    return true;
    // return false;
    } 
