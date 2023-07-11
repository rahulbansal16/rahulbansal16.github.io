---
layout: post
title: JavaScript Interview Questions
visible: 1
summary: "Tricky JS Interview Questions"
---

### Question1
Make changes to the following function so that the 1 invocation of the setInterval prints the same random number and next iteration different number.

You can only change the random method,
You can not change the callback inside the setInterval.

```javascript
const random = () => {
    return Math.random()
}
setInterval(() => {
  console.log(">>>>>")
  console.log(random())
  console.log(random())
  console.log("<<<<")
}, 3000)
```
Output should be 
```javascript
>>>>>
0.4343
0.4343
<<<<<
>>>>>
0.3624
0.3624
<<<<<
.....
```


### Solution
```javascript
let r = Math.random()
function random() {
  setTimeout (() => {
    r =  Math.random()
  }, 0)
  return r
}

setInterval(() => {
  console.log(">>>>>")
  console.log(random())
  console.log(random())
  console.log("<<<<")
}, 3000)
```

### Question 2
Implement the Typewriter effect on a string.

Refer to the codesandbox https://codesandbox.io/s/stoic-moon-n4xdm3
```javascript
import "./styles.css";
import { useEffect, useState } from "react";

export default function App() {
  return (
    <div className="App">
        <Typewriter text="Hello World" />
    </div>
  );
}

const Typewriter = ({ text }) => {
  const [index, setIndex] = useState(0);
  useEffect(() => {
    const intervalId = setInterval(() => {
      setIndex((prevIndex) => {
        if (prevIndex >= text.length) {
          clearInterval(intervalId);
        }
        return prevIndex + 1;
      });
    }, 500);
    return () => clearInterval(intervalId);
  }, [text]);

  return <div>Loaded: {text.substring(0, index)}</div>;
};
```
