# Redux-ReduxToolkit
Redux and Redux-toolkit 101.

What is Prop Drilling ?
![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/8ff478da-6f86-4095-938d-9a7172045d74)
For the data in the A component to be accessed in the C component, it has to be passed down as prop to the B component, and then finally the C component. This is known as threading.

Prop drilling does have its downsides, and in some cases it isn’t worth it. As your codebase increases, prop drilling can make your code overly complicated, and this can only get worse with more additions.

In addition to this, props can be passed down to components that don’t necessarily need it just for the data to get to the child component, leading to an unnecessary increase in the codebase.


So, to solve this ,we uses the State management libraries like ReduxJS/Redux-Toolkit or ContextAPI.


# REDUXJS :

Below is the Basic Visual takeaways to understand the terms in Redux.

![image](https://github.com/yash-devop/Redux-ReduxToolkit/assets/112558970/75198e95-5b63-4c3a-beb0-5a9a59f82266)

In Redux , we have 1) Actions 2) Store 3) Type 4)Payload 5) Reducer

In the above example : 
1) Action : We are depositing 100rs to the Bank(Store)..   what you want to do is 'Action' in redux.
2) Store : here , Bank is the store... means the basic storage of the values.
3) Type: In actions , we are Depositing the 100rs to the store right? so just we need a format to send the data to the store(bank)
   The FORMAT is :     action    ```type : payload``` where type is the Key and Payload is the Value or can say the Data to be send(i.e 100rs)
