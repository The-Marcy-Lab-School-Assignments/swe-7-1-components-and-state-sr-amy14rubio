# Short Response: Intro to React, Components, and useState

Answer each question below. Write in complete sentences (3–5 per answer).

---

## Question 1 — Components and JSX

What is a React component, and what is JSX? Explain how JSX differs from plain HTML. Use a brief code example to support your answer.

**Your answer:**
A React component is a **function** that is a **reusable piece of UI**. JSX is a syntax extension for JavaScript that allows developers to **write HTML-like code in React**. JSX differs from HTML as it allows for the combination of **JavaScript embedded into HTML-like syntax**. For example, if you were to style a button in HTML you would style it like this:

```html
<button style="border: 1px solid blue, color: blue">Click me</button>
```

While in JSX it would be written like this:

```jsx
<button style={{ border: '1px solid blue', color: 'blue' }}>Click me </button>
```

---

## Question 2 — The Build Step and Vite

A browser cannot run a `.jsx` file directly. Why not? Explain the role of a build step and what it means to "compile" code in simple terms.

**Your answer:**
A browser cannot run a `.jsx` file directly because while `.jsx` is in an easy and understandable language for the developer, it is not as readable for the browser. **The browser can only understand plain JavaScript**, to "compile" code means that the code is translated into plain JavaScript that can be processed by the browser. The role of the build step is to **compile** the `.jsx` file into a `.js` file and write everything to a `dist` folder, ready to be deployed.

---

## Question 3 — useState

What does `useState` return, and what are the two things you get back from it? Describe how to use those values to render data and to update that data.

**Your answer:**
`useState` returns a tuple with a **state value** and a **setter function** that triggers the re-render of the state value in a component. The state value stores the **current data** that should be displayed on the screen. The setter function is used to **update the state value** whenever changes need to be made. When the setter function is called, React re-renders the component with the updated data.

---

## Question 4 — Lifting State Up

What does it mean to "lift state up," and when is it necessary? Use a concrete example.

**Your answer:**
To "lift state up" means that a state that is defined in a **parent component can be passed down to its child component**. This is necessary when state needs to be shared or tracked across **multiple components**. An example of this would be having to keep track of a history of selected languages. To do so, you would need a `useState` array defining `history` and `setHistory`. When a language is selected, `setHistory` triggers a re-render of the `history` state even though the update happened in a different component.

---

## Question 5 — Bug Fix

The component below has a bug. When the user clicks "Add Cherries," the list never updates on screen. Identify what is wrong, write the corrected code, and explain **why** the original code fails in React.

```jsx
const ShoppingList = () => {
  const [items, setItems] = useState(['apples', 'bananas']);

  const addItem = () => {
    items.push('cherries');
    setItems(items);
  };

  return (
    <>
      <ul>
        {items.map((item, i) => (
          <li key={i}>{item}</li>
        ))}
      </ul>
      <button onClick={addItem}>Add Cherries</button>
    </>
  );
};
```

**Your answer:**
The list never updates on the screen because even though the `items` array was modified, it was **never re-rendered with a new array reference**. This means that even though `setItems(items)` is declared, `items` still references the **original array** and React can only re-render when a **new value** is given. In order to correctly solve this issue, `setItems` must create a copy of the `items` array and add `cherries` to the end of that copy in order to appropriately re-render the items array.

```jsx
const ShoppingList = () => {
  const [items, setItems] = useState(['apples', 'bananas']);

  const addItem = () => {
    setItems((items) => [...items, 'cherries']);
  };

  return (
    <>
      <ul>
        {items.map((item, i) => (
          <li key={i}>{item}</li>
        ))}
      </ul>
      <button onClick={addItem}>Add Cherries</button>
    </>
  );
};
```

---
