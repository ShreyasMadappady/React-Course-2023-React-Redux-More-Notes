# Yet Another Hook: useReducer
**Notes on the useReducer hook in React:**

* The `useReducer` hook is a more advanced way of managing state than the `useState` hook.
* It works with a reducer function, which is a pure function that takes the previous state and an action as arguments and returns the next state.
* The `useReducer` hook returns the current state and a dispatch function.
* To update the state, you dispatch an action, which is an object with a type property and a payload property.
* The reducer function will then decide what to do with the action and return the next state.

**Code example:**

```javascript
import React, { useReducer } from "react";

const initialState = {
  count: 0,
};

const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return {
        ...state,
        count: state.count + 1,
      };
    case "decrement":
      return {
        ...state,
        count: state.count - 1,
      };
    case "set_count":
      return {
        ...state,
        count: action.payload,
      };
    default:
      return state;
  }
};

const App = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h1>Counter</h1>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>Increment</button>
      <button onClick={() => dispatch({ type: "decrement" })}>Decrement</button>
      <input
        type="number"
        value={state.count}
        onChange={(e) => dispatch({ type: "set_count", payload: e.target.value })}
      />
    </div>
  );
};

export default App;
```

**Benefits of using the useReducer hook:**

* The `useReducer` hook is more scalable than the `useState` hook, especially when you have complex state logic or when the next state depends on the previous one.
* It is also more performant than the `useState` hook in some cases.

**When to use the useReducer hook:**

* You should use the `useReducer` hook when you have complex state logic or when the next state depends on the previous one.
* You should also use the `useReducer` hook when you need to improve the performance of your component.

**Conclusion:**

The `useReducer` hook is a powerful tool for managing state in React. It is more scalable and performant than the `useState` hook, but it can also be more complex to use. If you are new to React, I recommend starting with the `useState` hook and then moving to the `useReducer` hook as needed.

# Managing Related Pieces of State

**Detailed notes with code from the paragraph:**

**Incorporating the step state into the reducer:**

* We need to update the initial state to also include the step property:

```javascript
const initialState = {
  count: 0,
  step: 1,
};
```

* We need to update the reducer function to handle the `set_step` action:

```javascript
const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return {
        ...state,
        count: state.count + state.step,
      };
    case "decrement":
      return {
        ...state,
        count: state.count - state.step,
      };
    case "set_count":
      return {
        ...state,
        count: action.payload,
      };
    case "set_step":
      return {
        ...state,
        step: action.payload,
      };
    default:
      throw new Error("Unknown action");
  }
};
```

* We need to update the event handlers to dispatch the `set_step` action:

```javascript
function handleIncrement() {
  dispatch({ type: "increment" });
}

function handleDecrement() {
  dispatch({ type: "decrement" });
}

function handleSetStep() {
  const step = parseInt(event.target.value);
  dispatch({ type: "set_step", payload: step });
}
```

**Resetting the state:**

* We can add a new `reset` action to the reducer function:

```javascript
const reducer = (state, action) => {
  switch (action.type) {
    // ...
    case "reset":
      return initialState;
  }
};
```

* We can add a new event handler to dispatch the `reset` action:

```javascript
function handleReset() {
  dispatch({ type: "reset" });
}
```

**Benefits of the useReducer hook:**

* The useReducer hook is more scalable than the useState hook, especially when you have complex state logic or when the next state depends on the previous one.
* It is also more performant than the useState hook in some cases.
* The useReducer hook also makes it easier to understand and maintain your code, as all of the state logic is centralized in one place.

**Conclusion:**

The useReducer hook is a powerful tool for managing state in React. It is especially useful for complex applications, but it can also be used in simpler applications to improve scalability, performance, and maintainability.

# Managing State With useReducer

**Summary of the paragraph:**

The paragraph discusses the concept of reducers in React and how they can be used to manage state in a more efficient and scalable way than the useState hook. Reducers are especially useful for complex state and for related pieces of state.

**Key points:**

* A reducer is a function that takes in the current state and an action, and based on those values, returns the next state, so the updated state.
* Reducers must be pure functions, meaning they cannot mutate the state or have any side effects.
* Actions are objects that describe how state should be updated. They typically contain an action type and a payload, which is basically input data.
* The useReducer hook returns a state object and a dispatch function.
* To trigger a state update, you dispatch an action to the reducer using the dispatch function.
* Reducers are similar to the array reduce method in that they accumulate all actions into one single state over time.

**Benefits of using reducers:**

* Reducers are more scalable than the useState hook, especially when you have complex state logic or when the next state depends on the previous one.
* Reducers are also more performant than the useState hook in some cases.
* Reducers make it easier to understand and maintain your code, as all of the state logic is centralized in one place.

**When to use reducers:**

* You should use reducers when you have complex state or when the next state depends on the previous one.
* You should also use reducers when you need to improve the performance of your application.

**Analogy:**

The paragraph concludes with an analogy to the process of withdrawing money from a bank account. The bank vault represents the state, the customer represents the dispatcher, the teller represents the reducer, and the withdrawal request represents the action.

**Overall, the paragraph provides a clear and concise explanation of reducers in React and their benefits.**

# Loading Questions from a Fake API

## Summary of the paragraph

The paragraph describes the steps involved in setting up a fake API using json-server to load questions data into a React application. It also introduces the concept of using the useReducer hook to manage state in a more efficient and scalable way.

## Key points

* json-server is an npm package that can be used to create a fake API from a JSON file.
* The useReducer hook is a React hook that can be used to manage state in a more efficient and scalable way than the useState hook.
* Reducers are pure functions that take in the current state and an action, and return the next state.
* Actions are objects that describe how state should be updated.
* Reducers are useful for managing complex state or for related pieces of state.

## Steps to set up a fake API using json-server

1. Install json-server using npm: `npm install json-server`
2. Create a new folder for the API data, and place the JSON file containing the data in that folder.
3. Start the json-server server: `json-server --watch data/<JSON file>`
4. In your React application, use the fetch API to fetch the data from the json-server server.

## Steps to use the useReducer hook to manage state

1. Create a reducer function that takes in the current state and an action, and returns the next state.
2. Use the useReducer hook to get the state object and the dispatch function.
3. Use the dispatch function to dispatch actions to the reducer.
4. The reducer will update the state based on the action it receives.
5. The component will re-render whenever the state changes.

## Benefits of using the useReducer hook

* Reducers are more efficient and scalable than the useState hook, especially when you have complex state logic or when the next state depends on the previous one.
* Reducers make it easier to understand and maintain your code, as all of the state logic is centralized in one place.

## Example of using the useReducer hook to manage state

```javascript
// Reducer function
const reducer = (state, action) => {
  switch (action.type) {
    case "dataReceived":
      return {
        ...state,
        questions: action.payload,
        status: "ready",
      };
    case "dataFailed":
      return {
        ...state,
        status: "error",
      };
    default:
      throw new Error("Unknown action");
  }
};

// Component
const MyComponent = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  // Fetch the data from the json-server server
  useEffect(() => {
    fetch("http://localhost:8000/questions")
      .then(response => response.json())
      .then(data => dispatch({ type: "dataReceived", payload: data }))
      .catch(error => dispatch({ type: "dataFailed" }));
  }, []);

  // Display the data
  if (state.status === "ready") {
    return (
      <ul>
        {state.questions.map(question => (
          <li key={question.id}>{question.text}</li>
        ))}
      </ul>
    );
  } else if (state.status === "error") {
    return <div>Error fetching questions</div>;
  } else {
    return <div>Loading...</div>;
  }
};
```

## Conclusion

The useReducer hook is a powerful tool for managing state in React. It is especially useful for complex applications, but it can also be used in simpler applications to improve scalability, performance, and maintainability.

# Handling Loading, Error, and Ready Status

**Notes with code from the given paragraph:**

The paragraph describes how to handle the different statuses of a React application in the context of a quiz. The three statuses are:

* **Loading:** This is the initial state of the application, while it is fetching the quiz questions.
* **Ready:** This state is reached when the quiz questions have been fetched and the application is ready to start the quiz.
* **Error:** This state is reached if there is an error fetching the quiz questions or otherwise starting the quiz.

To handle these different statuses, the paragraph recommends using conditional rendering. This means using a ternary operator or `if` statement to render different components depending on the current state of the application.

For example, the following code shows how to render different components depending on the `status` state variable:

```javascript
const status = useState("loading");

return (
  <div>
    {status === "loading" && <Loader />}
    {status === "ready" && <StartScreen />}
    {status === "error" && <Error />}
  </div>
);
```

The `Loader`, `StartScreen`, and `Error` components are all React components that render different UIs for the corresponding state.

The paragraph also recommends using derived state to calculate the number of quiz questions. This means calculating the number of questions from the `questions` array instead of storing it as a separate state variable.

The following code shows how to use derived state to calculate the number of quiz questions:

```javascript
const questions = useState([
  // Quiz questions
]);

const numQuestions = derivedState(() => questions.length);

return (
  <StartScreen numQuestions={numQuestions} />
);
```

The `derivedState` function is a custom hook that can be used to calculate derived state. It takes a function as an argument, which calculates the derived state value. The derived state value is then returned from the `derivedState` function.

Finally, the paragraph mentions that the next lecture will cover how to start the quiz when the user clicks the "Let's start" button.

# Setting Up a Timer With useEffect

**Notes with code from the paragraph given below:**

The paragraph describes how to implement a timer feature in a React application using a reducer and a cleanup function.

**Steps:**

1. Add a new state variable to the reducer to track the remaining seconds.
```javascript
// reducer.js
export const reducer = (state, action) => {
  switch (action.type) {
    case "tick": {
      return {
        ...state,
        secondsRemaining: state.secondsRemaining - 1,
      };
    }
    default:
      return state;
  }
};
```

2. Add a new action type to the reducer to dispatch when the timer ticks.
```javascript
// reducer.js
export const reducer = (state, action) => {
  switch (action.type) {
    case "tick": {
      return {
        ...state,
        secondsRemaining: state.secondsRemaining - 1,
      };
    }
    case "finish": {
      return {
        ...state,
        status: "finished",
      };
    }
    default:
      return state;
  }
};
```

3. Add a new action type to the reducer to dispatch when the game finishes.
```javascript
// reducer.js
export const reducer = (state, action) => {
  switch (action.type) {
    case "tick": {
      return {
        ...state,
        secondsRemaining: state.secondsRemaining - 1,
      };
    }
    case "finish": {
      return {
        ...state,
        status: "finished",
      };
    }
    default:
      return state;
  }
};
```

4. Dispatch the `tick` action every second in the timer component using a cleanup function.
```javascript
// Timer.js
import { useDispatch } from "react-redux";

const Timer = ({ secondsRemaining }) => {
  const dispatch = useDispatch();

  const intervalId = useRef();

  useEffect(() => {
    intervalId.current = setInterval(() => {
      dispatch({ type: "tick" });
    }, 1000);

    return () => {
      clearInterval(intervalId.current);
    };
  }, []);

  return <div>{secondsRemaining}</div>;
};
```

5. Check if the seconds remaining are equal to zero in the reducer and dispatch the `finish` action if so.
```javascript
// reducer.js
export const reducer = (state, action) => {
  switch (action.type) {
    case "tick": {
      return {
        ...state,
        secondsRemaining: state.secondsRemaining - 1,
      };
    }
    case "finish": {
      return {
        ...state,
        status: "finished",
      };
    }
    default:
      return state;
  }
};
```

6. Render the finished screen when the status is equal to `finished`.
```javascript
// App.js
import { useSelector } from "react-redux";
import Timer from "./Timer";

const App = () => {
  const { status } = useSelector((state) => state);

  if (status === "finished") {
    return <div>Game over!</div>;
  }

  return <div>
    <Timer />
  </div>;
};
```

This code will implement a timer feature in the React application. The timer will tick every second and the game will finish when the seconds remaining are equal to zero.

# useState vs. useReducer

**Notes with code from the paragraph given below:**

The paragraph compares `useState` and `useReducer` and provides a framework for deciding which one to use.

**useState vs. useReducer**

| Feature | useState | useReducer |
|---|---|---|
| Ideal for | Single pieces of state that are independent from each other | Multiple pieces of state that are related and dependent on each other or complex state |
| State updating logic | Placed in event handlers or effects, spread all over the component or even located in child components if using lifted state | Centralized in one place, the reducer function |
| State updates | Feel more imperative | Feel more declarative |
| Easy to understand and use | Yes | No, requires writing a reducer function |

**Framework for deciding between useState and useReducer**

1. **Do you only need one piece of state?**
    * If yes, use `useState`.
2. **Do your states frequently need to be updated together?**
    * If yes, consider using `useReducer`.
3. **Are you willing to write a reducer function?**
    * If no, keep using `useState`.
4. **Do you need more than three or four pieces of related state, including objects?**
    * If yes, and you are willing to write a reducer, use `useReducer`.
5. **Do you have too many event handlers that make your components too large and confusing?**
    * If yes, consider using `useReducer`.
6. **If the answer to any of the above questions is no, then use `useState`.**

**Conclusion**

`useState` should be your default choice for managing React state. However, if `useState` gives you any of the problems discussed above, then consider using `useReducer`.

**Example**

In the game example mentioned in the paragraph, we need to update three pieces of state together (status, questions, and currentQuestion) when the user starts a new game. We are also willing to write a reducer function to handle this state update. Therefore, we would use `useReducer` in this case.

**Code example**

```javascript
// reducer.js
export const reducer = (state, action) => {
  switch (action.type) {
    case "startGame": {
      return {
        ...state,
        status: "active",
        questions: questions,
        currentQuestion: 0,
      };
    }
    default:
      return state;
  }
};

// App.js
import { useSelector, useDispatch } from "react-redux";

const App = () => {
  const dispatch = useDispatch();
  const { status } = useSelector((state) => state);

  if (status === "active") {
    // Render the game
  } else {
    // Render the start screen
  }

  return (
    <div>
      <button onClick={() => dispatch({ type: "startGame" })}>Start Game</button>
    </div>
  );
};
```

In this example, we use `useReducer` to manage the state of the game. The reducer function has a single case, `startGame`, which updates the state to start the game. We dispatch the `startGame` action from the start screen button.

**Conclusion**

`useReducer` is a powerful tool for managing complex state in React applications. However, it can be more difficult to understand and use than `useState`. Therefore, it is important to choose the right tool for the job. Use the framework above to help you decide whether to use `useState` or `useReducer`.


