# what is hooks ? 
- hooks are special functions, that allow use state and other react features in functional components.
- Earlier, when we used to create react app using Function component, then we didn't have access to the state management and lifecycle methods.
To access these features we had to add class components.
- so this was the problem with functional component.
- But after introducing React hooks from version 16.8, we can now use state management and other react features without writing class components.
- In other words, Hooks are the functions that make functional components work like class components.

What are the rules of hooks ?
1. Only call hooks at the top level and from react functional components.

Commonly Used Hooks:
- State Hooks (useState, useReducer)
- Effect Hooks (useEffect): Interact with external systems (e.g., API calls).
- Ref Hooks (useRef): Access DOM elements.

- useMemo, useCallback, useContext,useLayoutEffect, custom hook

## useState 
- useState is a react hook, which creates an "state variable". which helps us to track state in components and updates the user interface when state changes.
- useState returns an array with two elements. The first element is the current state value, and the second element is a function that lets you update it.
- useState is a named export from the react package.
- useState is a function that takes one argument, the initial state value, and returns an array with two elements.

### why useState is used ? 
=> example, 
```jsx
import { useState } from "react";
import "./App.css";

function App() {
	let color = "Red"
	const changeColor = () =>{
		color = "Blue"
		console.log(color)
	}
	return (
		<>
		<h1>My favorite color is {color}!</h1>
		<button onClick={changeColor}>Blue</button>
		</>
	)
}

export default App;
```

![alt text](image.png)
![alt text](image-1.png)

the images and codes shows why, we need useState hook. because, after making the button click, the color is not changing.

so, to solve this problem, we need to use useState hook.

```jsx
import { useState } from "react";
import "./App.css";

function App() {
	const counter = useState(0) // 0 is the initial value of the state variable. 
	console.log(counter) // [0, f] => 0 is the current state value, and f is the function that lets you update it.
    // or we can write like that... 

    const counter = useState(0)[0]
    const setCounter = useState(0)[1]


	let color = "Red"
	const changeColor = () =>{
		color = "Blue"
		// console.log(color)
	}
	return (
		<>
		<h1>My favorite color is {color}!</h1>
		<button onClick={changeColor}>Blue</button>
		</>
	)
}

export default App;

```

![alt text](image-2.png)

- Now, move to the next step, to use it effectively and efficiently syntax.
so, use array, of 2 elements to store the state variable and the function that updates it.

```jsx
import { useState } from "react";
import "./App.css";

function App() {
	const [counter, setCounter] = useState(10)
	console.log(counter)

	let color = "Red"
	const changeColor = () =>{
		color = "Blue"
		// console.log(color)
	}
	return (
		<>
		<h1>My favorite color is {color}!</h1>
		<button onClick={changeColor}>Blue</button>
		</>
	)
}

export default App;

```
![alt text](image-3.png)

```jsx
import { useState } from "react";
import "./App.css";

function App() {
	const [color, setColor] = useState("Red") 
	
	const changeColor = () =>{
		setColor("Blue")
	}
	return (
		<>
		<h1>My favorite color is {color}!</h1>
		<button onClick={changeColor}>Blue</button>
		</>
	)
}

export default App;

```
![alt text](image-4.png)

and when i click on button, it change the color from red to blue.

![alt text](image-5.png)

Now, play with multiple state variables

```jsx
import React,{useState} from 'react'

import './App.css';

function App() {
  const [brand, setBrand] = useState('ford') // multiple state variables 
  const [model, setModel] = useState('mustang')
  const [color, setColor] = useState('red')
  const [year, setYear] = useState(1964)

  return (
    <>
    <h1>my {brand}</h1>
    <h2>It is a {color} {model} from {year}</h2>
    </>
  );
}

export default App;
```

- instead of multiple state variables, we can use object to store the state variables as key-value pairs.

```jsx

import React,{useState} from 'react'

import './App.css';

function App() {
  const [car, setCar] = useState({ // key value pair
    brand: 'ford',
    model: 'mustang',
    color: 'red',
    year: 1964
  })

//   const changeColor = () => {
// 	setCar((prev)=>{
// 		return {...prev,color:'blue'}
// 	})
//   }

    const changeColor = () =>{
    setCar({...car, color: 'blue'}) 
  }

  return (
    <>
    <h1>my {car.brand}</h1>
    <h2>It is a {car.color} {car.model} from {car.year}</h2>
    <button onClick={changeColor}>blue</button>
    </>
  );
}

export default App;
```

### let's move on to the next example of useState which is counter button :)

-  increase by 1

```jsx
import React,{useState} from 'react'

import './App.css';

function App() {
  const [count,setCount] = useState(0)
  const increaseCount = () =>{
    setCount(count+1) 
  }
  return (
    <>
    <h1>count : {count}</h1>
    <button onClick={increaseCount}>Increment value</button>
    </>
  );
}

export default App;

```

- increase by 4 ? 

```jsx
import React,{useState} from 'react'

import './App.css';

function App() {
  const [count,setCount] = useState(0)
  const increaseCount = () =>{
    setCount(count+1) // 1 - it take initial value of count
    setCount(count+1) // 1 - it take initial value of count
    setCount(count+1) //1 - it take initial value of count
    setCount(count+1) //1 - it take initial value of count
  }
  return (
    <>
    <h1>count : {count}</h1>
    <button onClick={increaseCount}>Increment value</button>
    </>
  );
}

export default App;

```

### use previous state value for updating the state variable

```jsx
import React,{useState} from 'react'

import './App.css';

function App() {
  const [count,setCount] = useState(0)
  const increaseCount = () =>{
    setCount((prev)=>prev+1) // 0+1 = 1
    setCount((prev)=>prev+1) // 1+1 = 2
    setCount((prev)=>prev+1) // 2+1 = 3
    setCount((prev)=>prev+1) // 3+1 = 4
    // prev is the previous value of count and it is used to update the value of state 

  }
//   const increaseCount = () =>{
//     setCount(count+4)
//   }
  return (
    <>
    <h1>count : {count}</h1>
    <button onClick={increaseCount}>Increment value</button>
    </>
  );
}

export default App;

```

- prev is important to use, because it is used to update the state variable

# useEffect Hook 
- useEffect Hook allows you to perform side effects in your components
=> example : example of side effect is 
- fetching data from an API
- updating the DOM directly
- setting up a subscription
- Timers like SetTimeOut and SetInterval

1. import from react library
2. useEffect is a function that takes two arguments, a callback function and an array of dependencies (optional)
### 
ways to use useEffect (syntax)
1. useEffect(cb)
2. useEffect(cb, [])
3. useEffect(cb, [dependencies]) : useEffect(cb,[count,name,age,etc])

 ### example of useEffect - display a counter, that will how many times counter will loaded.

```jsx
import React,{useState, useEffect} from 'react'

import './App.css';

function App() {
  const [count, setCount] = useState(0)
  useEffect(()=>{ 
    setTimeout(()=>{
      setCount(prev => prev + 1) 
    },2000) // 2 seconds
  })
  return (
    <>
      <h1>I've rendered {count} times!</h1>
    </>
  );
}

export default App;

```

- Here is problem, it increase value from 0 to 2 directly, instead of 0 to 1, so, for this, just remove strict mode (`<React.StrictMode>`) from index.js file

![alt text](image-6.png)


comment out the strict mode from index.js file, and now, it will increase the value from 0 to 1 and so on.

## why this increase value continuously ?
- because, we are using useEffect without any dependencies, so it will run on every render, and it will increase the value of count.
- so, when we use useEffect without any dependencies, it will execute the call back function whenever the any state change in this component.
- so, the count state is changing in every 2 seconds and when the count state is changing it will again execute this callback function, so, it will increase the value of count continuously in every 2 seconds and update the count value state.

### 2nd example of useEffect - add dependencies, empty array 

```jsx
import React,{useState, useEffect} from 'react'

import './App.css';

function App() {
  const [count, setCount] = useState(0)
  useEffect(()=>{
    setTimeout(()=>{
      setCount(prev => prev + 1)
    },2000)
  },[])
  return (
    <>
      <h1>I've rendered {count} times!</h1>
    </>
  );
}

export default App;

```
- in empty array, useEffect will run only once, when the component is mounted, and it will not run again, because we have passed empty array as a second argument to useEffect.

### 3rd example of useEffect - add dependencies, array of count 

```jsx
import React,{useState, useEffect} from 'react'

import './App.css';

function App() {
  const [count, setCount] = useState(0)
  useEffect(()=>{
    setTimeout(()=>{
      setCount(prev => prev + 1)
    },2000)
  },[count])
  return (
    <>
      <h1>I've rendered {count} times!</h1>
    </>
  );
}

export default App;

```

- in this example, useEffect will run whenever the count state changes, because we have passed count as a dependency to useEffect.

### 4th example of useEffect - add dependencies, array of count and other state variables

```jsx
import React,{useState, useEffect} from 'react'

import './App.css';

function App() {
  const [count, setCount] = useState(0)
  const [name, setName] = useState('ar lab')
  useEffect(()=>{
    setTimeout(()=>{
      setCount(prev => prev + 1)
    },2000)
  },[count,name])
 // console.log(name)   
  return (
    <>
      <h1>I've rendered {count} times!</h1>
    </>
  );
}

export default App;

```

# useRef Hook

- useRef is react hook that allow us to create mutable variables, which will not re-render the component

- useRef is a react hook, which is used to access the DOM elements and also modified it and store the mutable value

=> example : create a count and display how many times it's re-rendered

```jsx
import React,{useState, useEffect, useRef} from 'react'

import './App.css';

function App() {
  const [value, setValue] = useState(0)
  const [cnt, setCnt] = useState(0)
  useEffect(()=>{
    setCnt(prev => prev+1)
  })
  return (
    <>
      <button onClick={()=>setValue(prev => prev-1)}>-1</button>
      <h1>{value}</h1>
      <button onClick={()=>setValue(prev => prev+1)}>+1</button>
      <h1>{cnt}</h1>
    </>
  );
}

export default App;

```
- cnt is increase continuously, because, it is re-rendering the component, so, to solve this problem, we need to use useRef hook.


```jsx
import React,{useState, useEffect, useRef} from 'react'

import './App.css';

function App() {
  const [value, setValue] = useState(0)
  // const [cnt, setCnt] = useState(0)
  const cnt = useRef(10)
  console.log(cnt)
  // useEffect(()=>{
  //   setCnt(prev => prev+1)
  // })
  return (
    <>
      <button onClick={()=>setValue(prev => prev-1)}>-1</button>
      <h1>{value}</h1>
      <button onClick={()=>setValue(prev => prev+1)}>+1</button>
      {/* <h1>{cnt}</h1> */}
    </>
  );
}

export default App;

```
![alt text](image-7.png)

- useRef is used as current property, so, to access the current value of the ref, we need to use current property.


```jsx
import React,{useState, useEffect, useRef} from 'react'

import './App.css';

function App() {
  const [value, setValue] = useState(0)
  const cnt = useRef(0)
  useEffect(()=>{
    cnt.current +=1
  })
  return (
    <>
      <button onClick={()=>setValue(prev => prev-1)}>-1</button>
      <h1>{value}</h1>
      <button onClick={()=>setValue(prev => prev+1)}>+1</button>
      <h1>{cnt.current}</h1>
    </>
  );
}

export default App;

```
- cnt is not increasing continuously, because, we are using useRef hook, so, it will not re-render the component, and it will not increase the value of cnt continuously.
- useRef is used to store the mutable value, and it will not re-render the component.
- useRef is used to access the DOM elements and also modified it.

### let's take example of useRef to access the DOM elements

```jsx
import React,{useState, useEffect, useRef} from 'react'

import './App.css';

function App() {
  const inputElement = useRef() // create a reference to input field
  const btnClicked = () =>{  
    console.log(inputElement.current)  
    inputElement.current.style.backgroundColor = 'red' // change the background color of input field
  }
  return (
    <>
    <input type="text" ref={inputElement} /> {/* assign the reference to input field */}
    <button onClick={btnClicked}> clicked me</button> {/* button to change the background color of input field */}
    </>
  );
}

export default App;

```