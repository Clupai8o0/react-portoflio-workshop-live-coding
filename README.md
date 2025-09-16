# React To-Do App — Step-by-Step (`App.js`)

*Live coding = incremental edits. Snippet = full copy-paste for that step.*
This mirrors your **Live coding** sequence and lands on the same final `App.js` you shared. &#x20;

---

## 0) Setup (from your live session)

**Live coding (terminal):**

```bash
# Create project
npx create-react-app todo-app
cd todo-app

# Tailwind CSS
npm install -D tailwindcss@3
npx tailwindcss init
```

> **Why:** CRA scaffolds React; Tailwind speeds styling with utility classes.&#x20;

**Snippet (config files):**

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"], // ← Scan src for class names
  theme: { extend: {} },
  plugins: [],
};
```

```css
/* src/index.css (or App.css if you prefer) */
@tailwind base;
@tailwind components;
@tailwind utilities;
/* ↑ Enables Tailwind layers the app uses later */
```

> **Why:** Ensures Tailwind classes used in components are picked up and compiled.&#x20;

---

## 1) Scaffold the page layout in `App.js`

**Live coding (edit `App.js`: add container, header, card, footer):**

```jsx
function App() {
  return (
    <div className="max-w-2xl mx-auto p-6 bg-gray-50 min-h-screen">
      <header className="text-center mb-8">
        <h1 className="text-4xl font-bold text-gray-800 mb-4">My Todo App</h1>
        <div className="flex justify-center gap-6 text-sm text-gray-600">
          {/* Stats area (we'll fill later) */}
        </div>
      </header>

      <main>
        <div className="bg-white rounded-xl shadow-lg p-6">
          {/* Todo app goes here */}
        </div>

        <footer className="text-center mt-8 text-gray-500 text-sm">
          <p>Built with React - Perfect for learning! 🚀</p>
        </footer>
      </main>
    </div>
  );
}
```

> **Comment:** Just the frame—no components yet. Uses Tailwind for quick, clean UI.&#x20;

**Snippet (copy-paste for this step):**

```jsx
import "./App.css";

function App() {
  return (
    <div className="max-w-2xl mx-auto p-6 bg-gray-50 min-h-screen">
      <header className="text-center mb-8">
        <h1 className="text-4xl font-bold text-gray-800 mb-4">My Todo App</h1>
        <div className="flex justify-center gap-6 text-sm text-gray-600">
          {/* Stats area (future) */}
        </div>
      </header>

      <main>
        <div className="bg-white rounded-xl shadow-lg p-6">
          {/* Todo app (future) */}
        </div>
        <footer className="text-center mt-8 text-gray-500 text-sm">
          <p>Built with React - Perfect for learning! 🚀</p>
        </footer>
      </main>
    </div>
  );
}
export default App;
```

---

## 2) Add component stubs: `TodoItem` + `TodoList`

**Live coding (create minimal stubs and mount list):**

```jsx
// Stubs we’ll flesh out soon
const TodoItem = () => {
  return <li className="p-4 bg-white rounded-lg mb-2 shadow-sm">Todo</li>;
};

const TodoList = () => {
  return (
    <ul className="space-y-0">
      <TodoItem />
      <TodoItem />
      <TodoItem />
    </ul>
  );
};

// Use the list inside the card
// ...
<div className="bg-white rounded-xl shadow-lg p-6">
  <TodoList />
</div>
```

> **Comment:** This proves the layout and spacing before wiring state/logic.&#x20;

**Snippet (copy-paste):**

```jsx
import "./App.css";

const TodoItem = () => (
  <li className="p-4 bg-white rounded-lg mb-2 shadow-sm">Todo</li>
);

const TodoList = () => (
  <ul className="space-y-0">
    <TodoItem />
    <TodoItem />
    <TodoItem />
  </ul>
);

function App() {
  return (
    <div className="max-w-2xl mx-auto p-6 bg-gray-50 min-h-screen">
      <header className="text-center mb-8">
        <h1 className="text-4xl font-bold text-gray-800 mb-4">My Todo App</h1>
        <div className="flex justify-center gap-6 text-sm text-gray-600">{/* Stats */}</div>
      </header>
      <main>
        <div className="bg-white rounded-xl shadow-lg p-6">
          <TodoList />
        </div>
        <footer className="text-center mt-8 text-gray-500 text-sm">
          <p>Built with React - Perfect for learning! 🚀</p>
        </footer>
      </main>
    </div>
  );
}
export default App;
```

---

## 3) Introduce stateful todos and render dynamically

**Live coding (add `useState` and map todos):**

```jsx
import { useState } from "react";

function App() {
  const [todos, setTodos] = useState([
    { id: 1, text: "Learn React basics", completed: true },
    { id: 2, text: "Build a todo app",   completed: false },
    { id: 3, text: "Practice state mgmt", completed: false },
  ]);
  // ...
}

// Make TodoList accept todos and map them
const TodoList = ({ todos }) => {
  return (
    <ul className="space-y-0">
      {todos.map((t) => (
        <TodoItem key={t.id} todo={t} />
      ))}
    </ul>
  );
};

// Update App to pass todos
// ...
<TodoList todos={todos} />
```

> **Comment:** We now have real data and unique keys—foundation for interactivity.&#x20;

**Snippet (copy-paste):**

```jsx
import "./App.css";
import { useState } from "react";

const TodoItem = ({ todo }) => (
  <li className="p-4 bg-white rounded-lg mb-2 shadow-sm">{todo.text}</li>
);

const TodoList = ({ todos }) => (
  <ul className="space-y-0">
    {todos.map((t) => (
      <TodoItem key={t.id} todo={t} />
    ))}
  </ul>
);

function App() {
  const [todos] = useState([
    { id: 1, text: "Learn React basics", completed: true },
    { id: 2, text: "Build a todo app", completed: false },
    { id: 3, text: "Practice state management", completed: false },
  ]);

  return (
    <div className="max-w-2xl mx-auto p-6 bg-gray-50 min-h-screen">
      <header className="text-center mb-8">
        <h1 className="text-4xl font-bold text-gray-800 mb-4">My Todo App</h1>
        <div className="flex justify-center gap-6 text-sm text-gray-600">{/* Stats */}</div>
      </header>
      <main>
        <div className="bg-white rounded-xl shadow-lg p-6">
          <TodoList todos={todos} />
        </div>
        <footer className="text-center mt-8 text-gray-500 text-sm">
          <p>Built with React - Perfect for learning! 🚀</p>
        </footer>
      </main>
    </div>
  );
}
export default App;
```

---

## 4) Style each item and prep for interactions

**Live coding (flesh out `TodoItem` visuals + check/delete controls):**

```jsx
const TodoItem = ({ todo }) => {
  return (
    <li
      className={`flex items-center gap-3 p-4 bg-white rounded-lg mb-2 shadow-sm hover:shadow-md transition-all duration-200 ${
        todo.completed ? "opacity-70" : ""
      }`}
    >
      <input
        type="checkbox"
        checked={todo.completed}         {/* UI reflects completed */}
        className="w-4 h-4 text-blue-500 rounded focus:ring-2 focus:ring-blue-300"
        /* onChange → wire up next step */
      />
      <span
        className={`flex-1 text-gray-800 ${
          todo.completed ? "line-through text-gray-500" : ""
        }`}
      >
        {todo.text}
      </span>
      <button
        className="px-3 py-1 bg-red-500 text-white text-sm rounded hover:bg-red-600 transition-colors"
        /* onClick → wire up next step */
      >
        Delete
      </button>
    </li>
  );
};
```

> **Comment:** Pure presentation now; the handlers come next.&#x20;

**Snippet (copy-paste):**

```jsx
import "./App.css";
import { useState } from "react";

const TodoItem = ({ todo }) => {
  return (
    <li className={`flex items-center gap-3 p-4 bg-white rounded-lg mb-2 shadow-sm hover:shadow-md transition-all duration-200 ${todo.completed ? "opacity-70" : ""}`}>
      <input type="checkbox" checked={todo.completed} className="w-4 h-4 text-blue-500 rounded focus:ring-2 focus:ring-blue-300" />
      <span className={`flex-1 text-gray-800 ${todo.completed ? "line-through text-gray-500" : ""}`}>{todo.text}</span>
      <button className="px-3 py-1 bg-red-500 text-white text-sm rounded hover:bg-red-600 transition-colors">Delete</button>
    </li>
  );
};

const TodoList = ({ todos }) => (
  <ul className="space-y-0">
    {todos.map((t) => (
      <TodoItem key={t.id} todo={t} />
    ))}
  </ul>
);

function App() {
  const [todos] = useState([
    { id: 1, text: "Learn React basics", completed: true },
    { id: 2, text: "Build a todo app", completed: false },
    { id: 3, text: "Practice state management", completed: false },
  ]);
  return (
    <div className="max-w-2xl mx-auto p-6 bg-gray-50 min-h-screen">
      <header className="text-center mb-8">
        <h1 className="text-4xl font-bold text-gray-800 mb-4">My Todo App</h1>
        <div className="flex justify-center gap-6 text-sm text-gray-600" />
      </header>
      <main>
        <div className="bg-white rounded-xl shadow-lg p-6">
          <TodoList todos={todos} />
        </div>
        <footer className="text-center mt-8 text-gray-500 text-sm">
          <p>Built with React - Perfect for learning! 🚀</p>
        </footer>
      </main>
    </div>
  );
}
export default App;
```

---

## 5) Toggle completion (checkbox)

**Live coding (add handler in App, pass down, use in item):**

```jsx
function App() {
  const [todos, setTodos] = useState([...]);

  const toggleTodo = (id) => {
    setTodos(todos.map((t) => (t.id === id ? { ...t, completed: !t.completed } : t)));
  };

  // Pass onToggle to list → item
  // ...
  <TodoList todos={todos} onToggle={toggleTodo} />
}

const TodoList = ({ todos, onToggle }) => (
  <ul className="space-y-0">
    {todos.map((t) => (
      <TodoItem key={t.id} todo={t} onToggle={onToggle} />
    ))}
  </ul>
);

const TodoItem = ({ todo, onToggle }) => (
  // ...
  <input
    type="checkbox"
    checked={todo.completed}
    onChange={() => onToggle(todo.id)}   {/* ← wire-up */}
    className="w-4 h-4 text-blue-500 rounded focus:ring-2 focus:ring-blue-300"
  />
  // ...
);
```

> **Comment:** Single source of truth in `App`; children receive functions via props.&#x20;

**Snippet (copy-paste)**: same as above with `toggleTodo` + prop threading.

---

## 6) Add tasks (`TodoForm` + `addTodo`)

**Live coding (new component, Enter key support, lift state update):**

```jsx
const TodoForm = ({ onAdd }) => {
  const [inputValue, setInputValue] = useState("");

  const handleSubmit = () => {
    if (inputValue.trim()) {
      onAdd(inputValue.trim());      // ask parent to add
      setInputValue("");             // clear field
    }
  };

  const handleKeyPress = (e) => {
    if (e.key === "Enter") handleSubmit();  // quick add on Enter
  };

  return (
    <div className="flex gap-2 mb-6">
      <input
        type="text"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
        onKeyPress={handleKeyPress}
        placeholder="Add a new task..."
        className="flex-1 px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-400 focus:outline-none text-gray-700"
      />
      <button onClick={handleSubmit} className="px-6 py-3 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors font-medium">
        Add Task
      </button>
    </div>
  );
};

function App() {
  const [todos, setTodos] = useState([...]);

  const addTodo = (text) => {
    const newTodo = { id: Date.now(), text, completed: false }; // demo id
    setTodos([...todos, newTodo]);
  };

  // Render form above the list
  // ...
  <div className="bg-white rounded-xl shadow-lg p-6">
    <TodoForm onAdd={addTodo} />
    <TodoList todos={todos} onToggle={toggleTodo} />
  </div>
}
```

> **Comment:** `TodoForm` manages its own input; `App` manages the todos array.&#x20;

**Snippet (copy-paste)**: same as above with `TodoForm` + `addTodo`.

---

## 7) Delete tasks

**Live coding (add `deleteTodo` and connect button):**

```jsx
function App() {
  // ...
  const deleteTodo = (id) => {
    setTodos(todos.filter((t) => t.id !== id));
  };

  <TodoList todos={todos} onToggle={toggleTodo} onDelete={deleteTodo} />
}

const TodoList = ({ todos, onToggle, onDelete }) => (
  <ul className="space-y-0">
    {todos.map((t) => (
      <TodoItem key={t.id} todo={t} onToggle={onToggle} onDelete={onDelete} />
    ))}
  </ul>
);

const TodoItem = ({ todo, onToggle, onDelete }) => (
  // ...
  <button
    className="px-3 py-1 bg-red-500 text-white text-sm rounded hover:bg-red-600 transition-colors"
    onClick={() => onDelete(todo.id)}     {/* ← remove */}
  >
    Delete
  </button>
);
```

> **Comment:** Pure functional updates—no mutation; React can diff and re-render efficiently.&#x20;

**Snippet (copy-paste)**: same as above with `deleteTodo`.

---

## 8) Filters + empty state polish

**Live coding (filter state + buttons + derived `filteredTodos`):**

```jsx
function App() {
  const [todos, setTodos] = useState([...]);
  const [filter, setFilter] = useState("all"); // "all" | "active" | "completed"

  const filteredTodos = todos.filter((t) => {
    if (filter === "active") return !t.completed;
    if (filter === "completed") return t.completed;
    return true;
  });

  // ...
  <FilterButtons currentFilter={filter} onFilterChange={setFilter} />
  <TodoList todos={filteredTodos} onToggle={toggleTodo} onDelete={deleteTodo} />
}

const FilterButtons = ({ currentFilter, onFilterChange }) => {
  const filters = ["all", "active", "completed"];
  return (
    <div className="flex justify-center gap-2 mb-4">
      {filters.map((f) => (
        <button
          key={f}
          className={`px-4 py-2 rounded-full border-2 transition-all ${
            currentFilter === f
              ? "bg-blue-500 text-white border-blue-500"
              : "bg-white text-gray-600 border-gray-200 hover:border-blue-400"
          }`}
          onClick={() => onFilterChange(f)}
        >
          {f.charAt(0).toUpperCase() + f.slice(1)}
        </button>
      ))}
    </div>
  );
};

// Empty state inside TodoList
const TodoList = ({ todos, onToggle, onDelete }) => {
  if (todos.length === 0) {
    return (
      <div className="text-center py-12">
        <p className="text-gray-500 italic text-lg">No tasks to display</p>
        <p className="text-gray-400 text-sm mt-2">Add a task above to get started!</p>
      </div>
    );
  }
  // ...
};
```

> **Comment:** Filter is derived UI state; empty state avoids a blank page and guides the user.&#x20;

**Snippet (copy-paste)**: same as above with `FilterButtons`, `filteredTodos`, and empty state branch.

---

## 9) (Optional) Header stats

**Live coding (compute basic counts and show them):**

```jsx
const totalTodos = todos.length;
const completedTodos = todos.filter((t) => t.completed).length;
const activeTodos = totalTodos - completedTodos;

// In header:
<div className="flex justify-center gap-6 text-sm text-gray-600">
  <span className="bg-white px-3 py-1 rounded-full shadow-sm"><strong>Total:</strong> {totalTodos}</span>
  <span className="bg-white px-3 py-1 rounded-full shadow-sm"><strong>Active:</strong> {activeTodos}</span>
  <span className="bg-white px-3 py-1 rounded-full shadow-sm"><strong>Completed:</strong> {completedTodos}</span>
</div>
```

> **Comment:** Nice UX touch for a “finished” feel, easy to remove if not needed.&#x20;

---

## ✅ Final `App.js` (matches your file)

**Snippet (full copy-paste):**

```jsx
import "./App.css";
import { useState } from "react";

const TodoItem = ({ todo, onToggle, onDelete }) => {
  return (
    <li
      className={`flex items-center gap-3 p-4 bg-white rounded-lg mb-2 shadow-sm hover:shadow-md transition-all duration-200 ${
        todo.completed ? "opacity-70" : ""
      }`}
    >
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={() => onToggle(todo.id)}
        className="w-4 h-4 text-blue-500 rounded focus:ring-2 focus:ring-blue-300"
      />
      <span
        className={`flex-1 text-gray-800 ${
          todo.completed ? "line-through text-gray-500" : ""
        }`}
      >
        {todo.text}
      </span>
      <button
        className="px-3 py-1 bg-red-500 text-white text-sm rounded hover:bg-red-600 transition-colors"
        onClick={() => onDelete(todo.id)}
      >
        Delete
      </button>
    </li>
  );
};

const TodoList = ({ todos, onToggle, onDelete }) => {
  if (todos.length === 0) {
    return (
      <div className="text-center py-12">
        <p className="text-gray-500 italic text-lg">No tasks to display</p>
        <p className="text-gray-400 text-sm mt-2">
          Add a task above to get started!
        </p>
      </div>
    );
  }

  return (
    <ul className="space-y-0">
      {todos.map((todo) => (
        <TodoItem
          key={todo.id}
          todo={todo}
          onToggle={onToggle}
          onDelete={onDelete}
        />
      ))}
    </ul>
  );
};

const TodoForm = ({ onAdd }) => {
  const [inputValue, setInputValue] = useState("");

  const handleSubmit = () => {
    if (inputValue.trim()) {
      onAdd(inputValue.trim());
      setInputValue("");
    }
  };

  const handleKeyPress = (e) => {
    if (e.key === "Enter") {
      handleSubmit();
    }
  };

  return (
    <div className="flex gap-2 mb-6">
      <input
        type="text"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
        onKeyPress={handleKeyPress}
        placeholder="Add a new task..."
        className="flex-1 px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-400 focus:outline-none text-gray-700"
      />
      <button
        onClick={handleSubmit}
        className="px-6 py-3 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors font-medium"
      >
        Add Task
      </button>
    </div>
  );
};

const FilterButtons = ({ currentFilter, onFilterChange }) => {
  const filters = ["all", "active", "completed"];
  return (
    <div className="flex justify-center gap-2 mb-4">
      {filters.map((filter) => (
        <button
          key={filter}
          className={`px-4 py-2 rounded-full border-2 transition-all ${
            currentFilter === filter
              ? "bg-blue-500 text-white border-blue-500"
              : "bg-white text-gray-600 border-gray-200 hover:border-blue-400"
          }`}
          onClick={() => onFilterChange(filter)}
        >
          {filter.charAt(0).toUpperCase() + filter.slice(1)}
        </button>
      ))}
    </div>
  );
};

function App() {
  const [todos, setTodos] = useState([
    { id: 1, text: "Learn React basics", completed: true },
    { id: 2, text: "Build a todo app", completed: false },
    { id: 3, text: "Practice state management", completed: false },
  ]);
  const [filter, setFilter] = useState("all");

  const addTodo = (text) => {
    const newTodo = { id: Date.now(), text, completed: false };
    setTodos([...todos, newTodo]);
  };

  const toggleTodo = (id) => {
    setTodos(
      todos.map((todo) =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };

  const deleteTodo = (id) => {
    setTodos(todos.filter((todo) => todo.id !== id));
  };

  const filteredTodos = todos.filter((todo) => {
    if (filter === "active") return !todo.completed;
    if (filter === "completed") return todo.completed;
    return true;
  });

  // Optional header stats
  const totalTodos = todos.length;
  const completedTodos = todos.filter((t) => t.completed).length;
  const activeTodos = totalTodos - completedTodos;

  return (
    <div className="max-w-2xl mx-auto p-6 bg-gray-50 min-h-screen">
      <header className="text-center mb-8">
        <h1 className="text-4xl font-bold text-gray-800 mb-4">My Todo App</h1>
        <div className="flex justify-center gap-6 text-sm text-gray-600">
          {/* Stats */}
          <span className="bg-white px-3 py-1 rounded-full shadow-sm">
            <strong>Total:</strong> {totalTodos}
          </span>
          <span className="bg-white px-3 py-1 rounded-full shadow-sm">
            <strong>Active:</strong> {activeTodos}
          </span>
          <span className="bg-white px-3 py-1 rounded-full shadow-sm">
            <strong>Completed:</strong> {completedTodos}
          </span>
        </div>
      </header>

      <main>
        <div className="bg-white rounded-xl shadow-lg p-6">
          <TodoForm onAdd={addTodo} />
          <FilterButtons currentFilter={filter} onFilterChange={setFilter} />
          <TodoList
            todos={filteredTodos}
            onToggle={toggleTodo}
            onDelete={deleteTodo}
          />
        </div>

        <footer className="text-center mt-8 text-gray-500 text-sm">
          <p>Built with React - Perfect for learning! 🚀</p>
        </footer>
      </main>
    </div>
  );
}
export default App;
```

> **Comment:** This final file is identical in structure/behavior to your shared `App.js`.&#x20;

## 🙌 Credits & Bug Hunt

* Credits to **Shalok** — if this helped, please **⭐ star** the repo: `https://github.com/Shalok-sys/DSEC_TO_DO_APP/`
* 
Think you know enough? Join the **workshop bug hunt** here: `https://github.com/Shalok-sys/DSEC_TO_DO_APP/tree/workshop-bugs`
