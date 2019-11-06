---
id: state
title: State
---

There are two types of data that control a component: `props` and `state`. `props` are set by the parent and they are fixed throughout the lifetime of a component. For data that is going to change, we have to use `state`.

In general, you should initialize `state` with useState. Which gives you the `variable` and a `setVariable` function used to change the state. Not changing the state variable directly, but wby calling setVariableName.

In the example below: `const [showText, setShowText] = useState(true)`. The initial value of the state variable (showText in this example) will be whatever you put into useState(). `showText` is initialized as true, and changed in our useEffect hook to false, with the `setShowText()` function.

So let's say we want to make text that blinks all the time. The text itself gets set once when the blinking component gets created, so the text itself is a `prop`. The "whether the text is currently on or off" changes over time, so that should be kept in its `state`.

```SnackPlayer name=State
import React, { useState, useEffect } from 'react';
import { Text, View } from 'react-native';

const Blink = props => {
  // state hook
  const [showText, setShowText] = useState(true);

  useEffect(() => {
    // Toggle the state every second
    const interval = setInterval(() => setShowText(!showText), 1000);
    return () => clearInterval(interval);
  }, [showText]);

  if (!showText) {
    return null;
  } else {
    return <Text>{props.text}</Text>;
  }
};

const BlinkApp = () => {
  return (
    <View style={{ alignItems: 'center', top: 50 }}>
      <Blink text="I love to blink" />
      <Blink text="Yes blinking is so great" />
      <Blink text="Why did they ever take this out of HTML" />
      <Blink text="Look at me look at me look at me" />
    </View>
  );
};

export default BlinkApp;
```

In a real application, you probably won't be setting state with a timer. You might set state when you have new data from the server, or from user input. You can also use a state container like [Redux](https://redux.js.org/) or [Mobx](https://mobx.js.org/) to control your data flow. In that case you would use Redux or Mobx to modify your state rather than calling `setState` directly.

When setState is called, BlinkApp will re-render its Component. By calling setState within the Timer, the component will re-render every time the Timer ticks.

State works the same way as it does in React, so for more details on handling state, you can look at the [Hooks API Reference
](https://reactjs.org/docs/hooks-reference.html#usestate). At this point, you may have noticed that most of our examples use the default text color. To customize the text color, you will have to [learn about Style](style.md).
