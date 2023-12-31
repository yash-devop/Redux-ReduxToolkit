![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/9297e63a-5da2-4941-a5a2-f80cfede2b25)#                                                       Redux and Redux-toolkit 101.

What is Prop Drilling ?
![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/8ff478da-6f86-4095-938d-9a7172045d74)

For the data in the A component to be accessed in the C component, it has to be passed down as prop to the B component, and then finally the C component. This is known as threading.

Prop drilling does have its downsides, and in some cases it isn’t worth it. As your codebase increases, prop drilling can make your code overly complicated, and this can only get worse with more additions.

In addition to this, props can be passed down to components that don’t necessarily need it just for the data to get to the child component, leading to an unnecessary increase in the codebase.


So, to solve this ,we uses the State management libraries like ReduxJS/Redux-Toolkit or ContextAPI.


# REDUXJS :

Below is the Basic Visual takeaways to understand the terms in Redux.

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/75198e95-5b63-4c3a-beb0-5a9a59f82266)

In Redux , we have 1) Actions 2) Store 3) Type 4)Payload 5) Reducer 6) Dispatch

In the above example : 
1) Action : We are depositing 100rs to the Bank(Store)..   what you want to do is 'Action' in redux.
2) Store : here , Bank is the store... means the basic storage of the values.
3) Type: In actions , we are Depositing the 100rs to the store right? so just we need a format to send the data to the store(bank)
   The FORMAT is :     action    ```type : payload``` where type is the Key and Payload is the Value or can say the Data to be send(i.e 100rs)
4) Payload: the data/value that we are sending.
5) Reducer (imp): To update the store, we use the reducer .
   suppose , action is to add the 100rs to the store.
   So,basically it takes the state of the Bank(store) i.e 200rs as the previous state and adds the new value ie 100rs to the previous state.
   ```Previous state + Action ( 200 + 100 )```

   #Note: + is dependent on what type of action you are performing.. here i m doing addition that'y +

6) Dispatch : now how to send that functionality to the store ?? we need something to send that action to the store right ?
   so for example: we have a button , when we click it , it will do something like do API calls whatever....

   So , Dispatch is applied on something that will take that Action to the Store.

   Something can be : a button or anyyyy UI thing.


   # NPM Redux Install

   Do :  ``` npm install redux ```
   After this , create a file called index.js

   # 2 Methods to create " STORE " in Redux

   # 1) createStore
      
      ```js
      // import {createStore} from 'redux';
      const redux = require('redux')
      
      // createStore
      
      const initialState = {
          amount : 1
      }
      const store = redux.createStore(reducer);
      
      function reducer(state=initialState,action){
          // now,after line 24 ,this reducer function will have the access inside ACTION
          if(action.type === "INCREMENT"){ //this should match the exact type : "..."
              return {amount : initialState.amount+1}
          } 
          return state;
      }
      
      // get global state
      console.log(store.getState());  // provides us the GlobalState
      
      // action format : {type : "INCREMENT"};
      
      // Dispatch the action. so we have to use : dispatch() from store.
      // inside that we have to pass the object/data/action with format type:data
      
      store.dispatch({type: "INCREMENT"})
      
      // now will check whether changes took place or not
      
      console.log(store.getState());
      ```

      # Without Comments :
      ```js
      // import {createStore} from 'redux'   => for REACT
      const redux = require('redux')
      
      // createStore
      
      const initialState = {
          amount : 1
      }
      const store = redux.createStore(reducer);
      
      function reducer(state=initialState,action){
          if(action.type === "INCREMENT"){
              return {amount : initialState.amount+1}
          } 
          return state;
      }
      
      // get global state
      console.log(store.getState());

      store.dispatch({type: "INCREMENT"})
          
      console.log(store.getState());
      ```

   # Vscode Snippet :
   ![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/6b118d90-a78a-4275-86fa-192acb853287)
   ![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/a8c8f92b-0186-4dc8-8c10-077a21416b3f)


   # We can also apply Middlewares in Redux :

   Vscode snippet :
   ![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/372ebeda-6c0b-49e1-8554-dbf746f5f77d)
   ```js
   import {createStore , applyMiddleware} from 'redux';
   import logger from 'redux-logger';
   const initialState = {
       amount : 1
   }
   // if we are using REDUX in Node,  then just we have to write .default while
   // applying middleware
   const store = createStore(reducer , applyMiddleware(logger.default));
   
   function reducer(state=initialState,action){
       if(action.type === "INCREMENT"){ 
           return {amount : initialState.amount+1}
       } 
       return state;
   }
   
   console.log(store.getState()); 
   
   store.dispatch({type: "INCREMENT"})
   
   console.log(store.getState());
   ```

# Multiple Data:
![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/3f451f3e-f303-4c18-9c27-7f11b7213de0)

```js
      import {createStore , applyMiddleware} from 'redux';
      import logger from 'redux-logger';
      const initialState = {
          amount : 1
      }
      // if we are using REDUX in Node,  then just we have to write .default while
      // applying middleware
      const store = createStore(reducer , applyMiddleware(logger.default));
      function reducer(state=initialState,action){
          if(action.type === "INCREMENT"){ 
              return {amount : initialState.amount+1}
          }
          if(action.type === "DECREMENT"){
              return {amount : initialState.amount - 1};
          }
          if(action.type === "INCREMENTByAmount"){
              return {amount : initialState.amount + action.payload };
          }
          return state;
      }
      // store.dispatch({type: "DECREMENT"})  // decrement amount:1 to amount:0
      // store.dispatch({type: "INCREMENTByAmount"}) //this will not work, it will return NaN
      store.dispatch({type: "INCREMENTByAmount" , payload : 9}) 

```

This ACTIONS ```{type: "INCREMENTByAmount" , payload : 9}``` data can become complicated and need to simplify it.
so , we use ACTION CREATORS

```js
   import {createStore , applyMiddleware} from 'redux';
   import logger from 'redux-logger';
   const initialState = {
       amount : 1
   }
   // if we are using REDUX in Node,  then just we have to write .default while
   // applying middleware
   const store = createStore(reducer , applyMiddleware(logger.default));
   
   // Action Creator:
   
   const increment =()=>{
       return {type:"INCREMENT"}
   }
   const decrement =()=>{
       return {type:"DECREMENT"}
   }
   const INCREMENTByAmount =()=>{
       return {type:"INCREMENTByAmount" , payload : 9}
   }
   
   function reducer(state=initialState,action){
       if(action.type === "INCREMENT"){ 
           return {amount : initialState.amount+1}
       }
       if(action.type === "DECREMENT"){
           return {amount : initialState.amount - 1};
       }
       if(action.type === "INCREMENTByAmount"){
           return {amount : initialState.amount + action.payload };
       }
       return state;
   }
   store.dispatch(INCREMENTByAmount()) 

```

VSCODE SNIPPET :

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/164b4ec4-5534-4322-8d0b-f4111c53cae0)
![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/b901fcff-9a71-4192-963d-fb6463f8da12)

```js
      import {createStore , applyMiddleware} from 'redux';
      import logger from 'redux-logger';
      const initialState = {
          amount : 1
      }
      // if we are using REDUX in Node,  then just we have to write .default while
      // applying middleware
      const store = createStore(reducer , applyMiddleware(logger.default));
      
      // Action Creator:
      
      const increment =()=>{
          return {type:"INCREMENT"}
      }
      const decrement =()=>{
          return {type:"DECREMENT"}
      }
      const INCREMENTByAmount =(value)=>{
          return {type:"INCREMENTByAmount" , payload : value}
      }
      
      function reducer(state=initialState,action){
          if(action.type === "INCREMENT"){ 
              return {amount : initialState.amount+1}
          }
          if(action.type === "DECREMENT"){
              return {amount : initialState.amount - 1};
          }
          if(action.type === "INCREMENTByAmount"){
              return {amount : initialState.amount + action.payload };
          }
          return state;
      }
      store.dispatch(INCREMENTByAmount(9)) 

```

# Suppose we have to make an API call in Redux ( ** REDUX THUNK ** )

For now , i created a simple db.json file as my basic easy database which returns json.

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/c4efcf96-80cd-46fe-8a34-e5c2a39b3404)

Let's create a JSON server in node so that we can use it as an API.


![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/6ef6b0e0-17db-46f6-82f9-d9e73765c064)

Now type : ``` json-server db.json```  to start our json file as the server ... it will provide a link.

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/746fec96-29e7-42c8-b4f8-5917264655f0)

Now , Install Axios Library to make API calls ,fetch the data..

``` npm i axios```
  
Now we have to make API call and whatever the value it returns , we have to pass it to the REDUCER with actions(contains the data as we did in the above codes)

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/e980c54f-3388-486d-8ff5-33486c40e2e2)

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/3fc084b9-f70b-4807-9dd9-6c614137e454)


```js
   import {createStore , applyMiddleware} from 'redux';
   import logger from 'redux-logger';
   const initialState = {
       amount : 1
   }
   // if we are using REDUX in Node,  then just we have to write .default while
   // applying middleware
   const store = createStore(reducer , applyMiddleware(logger.default));
   
   // Action Creator:
   
   const initUser =(value)=>{
       return {type:"INITIAL" ,payload:value}
   }
   const increment =()=>{
       return {type:"INCREMENT"}
   }
   const decrement =()=>{
       return {type:"DECREMENT"}
   }
   const INCREMENTByAmount =(value)=>{
       return {type:"INCREMENTByAmount" , payload : value}
   }
   
   function reducer(state=initialState,action){
   
       switch(action.type){
           case "INITIAL":
               return {amount : action.payload};
           case "INCREMENT":
               return {amount : initialState.amount+1};
           case "DECREMENT":
               return {amount : initialState.amount-11};
           case "INCREMENTByAmount":
               return {amount : initialState.amount + action.payload};
           default:
               return state;
           
       }
   }
   store.dispatch(INCREMENTByAmount(899)) 


```

Now , we have to MAKE AN API CALL ,so will do :  ( in the Index.js node server file)

vscode snippet : 
![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/4f662292-fcc6-4caa-90a7-5c6411ca8957)

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/5815c6e7-8722-45cc-ad25-292432482c4c)

// API CALL

```js
const getUser=async()=>{
    const {data} = await axios.get('http://localhost:3000/account/1') 
    console.log(data)

}
store.dispatch(getUser()) 
```
It will THROW AN ERROR... Its a very common error in Redux coz we are making an API CALL and in redux we can achieve this by using REDUX THUNK

now , When we are using Redux Thunk , we have to pass the FUNCTION and not the Function Call in the Dispatch
like instead of ```store.dispatch(INCREMENTByAmount())```  , we have to pass ```store.dispatch(INCREMENTByAmount) ```
and also , we have to pass 2 parameters :  ```dispatch and getState ```in the function you are making the API CALLS

Vscode snippet: 
![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/395b5aab-d3fb-4894-b47d-85eac3acf184)

Code :

```js
// API CALL

const getUser=async(dispatch,getState)=>{
    const {data} = await axios.get('http://localhost:3000/account/1') 
    console.log(data)
    dispatch({type: initUser , payload: data.amount})

}
store.dispatch(getUser) 
```


Now in the above code,  we are passing that we want the data at ID = 1
but what if we do it dynamically , whatever the user passes , it should do that particular API CALL

Follow this : 

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/e0e87909-2e52-40e6-ba7d-19d7d364223e)

Code :

Here , we did some modification like we have the getUser function , just we have passed the id as the argument
and inside this getUser function , we are returning another function which is async and making the API CALL..

This is the best approach to make the API CALLS.


```js

// API CALL

const getUser=(id)=>{
    return async(dispatch,getState)=>{
        // const {data} = await axios.get(`http://localhost:3000/account/1`) 
        const {data} = await axios.get(`http://localhost:3000/account/${id}`) 
        console.log(data)
        dispatch({type: initUser , payload: data.amount})
    }

}
store.dispatch(getUser(2)) 

```

# Multiple Reducers 

Suppose , in our api we have other field as bonus:

