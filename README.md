This project involves building a simple To-Do List application using React. Below is a step-by-step breakdown of how to implement the application according to the requirements.

Step 1: Set up the project
To start, you'll need to set up a React app. If you haven't already, you can create one using create-react-app:

bash
Copy
npx create-react-app todo-app
cd todo-app
npm start
This will set up a basic React app, and you can begin adding the required components.

Step 2: Create Components
The app will consist of four components:

App Component: The main container for all components.
TodoList Component: Displays a list of tasks.
TodoItem Component: Displays individual tasks.
AddTodo Component: Allows users to input and add a new task.
Step 3: App Component
The App component will hold the state for the list of tasks and the input value. It will render the TodoList and AddTodo components.

jsx
Copy
import React, { useState } from 'react';
import TodoList from './TodoList';
import AddTodo from './AddTodo';

function App() {
  const [todos, setTodos] = useState([]);

  const addTodo = (task) => {
    if (task.trim() !== "") {
      const newTodo = {
        id: Date.now(),
        task,
        completed: false,
      };
      setTodos([...todos, newTodo]);
    }
  };

  const toggleComplete = (id) => {
    setTodos(
      todos.map((todo) =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };

  const deleteTodo = (id) => {
    setTodos(todos.filter((todo) => todo.id !== id));
  };

  return (
    <div className="App">
      <h1>To-Do List</h1>
      <AddTodo onAddTodo={addTodo} />
      <TodoList todos={todos} onToggleComplete={toggleComplete} onDeleteTodo={deleteTodo} />
    </div>
  );
}

export default App;
Step 4: AddTodo Component
The AddTodo component contains an input field and a button to add tasks. It will call the onAddTodo function passed from App when a new task is added.

jsx
Copy
import React, { useState } from 'react';

function AddTodo({ onAddTodo }) {
  const [input, setInput] = useState('');

  const handleInputChange = (e) => {
    setInput(e.target.value);
  };

  const handleAddClick = () => {
    onAddTodo(input);
    setInput('');
  };

  return (
    <div>
      <input
        type="text"
        value={input}
        onChange={handleInputChange}
        placeholder="Enter a new task"
      />
      <button onClick={handleAddClick}>Add Task</button>
    </div>
  );
}

export default AddTodo;
Step 5: TodoList Component
The TodoList component will receive the list of tasks and display them using the TodoItem component. It will also handle task completion and deletion.

jsx
Copy
import React from 'react';
import TodoItem from './TodoItem';

function TodoList({ todos, onToggleComplete, onDeleteTodo }) {
  return (
    <div>
      <ul>
        {todos.map((todo) => (
          <TodoItem
            key={todo.id}
            todo={todo}
            onToggleComplete={onToggleComplete}
            onDeleteTodo={onDeleteTodo}
          />
        ))}
      </ul>
    </div>
  );
}

export default TodoList;
Step 6: TodoItem Component
The TodoItem component represents each individual task. It will display the task text and have options to toggle completion and delete the task.

jsx
Copy
import React from 'react';

function TodoItem({ todo, onToggleComplete, onDeleteTodo }) {
  return (
    <li
      onClick={() => onToggleComplete(todo.id)}
      style={{
        textDecoration: todo.completed ? 'line-through' : 'none',
        backgroundColor: todo.completed ? '#d3ffd3' : 'white',
      }}
    >
      {todo.task}
      <button onClick={(e) => {
        e.stopPropagation(); // Prevent triggering onClick for task toggle
        onDeleteTodo(todo.id);
      }}>Delete</button>
    </li>
  );
}

export default TodoItem;
Step 7: Styling
Create a styles.css file to style the components. Add basic styling to make the app look neat.

css
Copy
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f1f1f1;
}

.App {
  width: 400px;
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
}

input {
  width: 70%;
  padding: 8px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 12px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 10px;
  border-bottom: 1px solid #ddd;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

li button {
  background-color: #f44336;
}

li button:hover {
  background-color: #e53935;
}
Step 8: Input Validation
The AddTodo component already includes input validation by checking if the task input is not empty. If it is empty, the addTodo function will not add the task.

Step 9: Putting it all together
Make sure to import the CSS into your App.js file:

jsx
Copy
import './styles.css';
Now, when you run the app (npm start), you will have the following features:

Add Task: Users can add new tasks.
Complete Task: Click on a task to mark it as completed.
Delete Task: Each task has a delete button to remove it from the list.
Conditional Rendering: Completed tasks will be visually different (crossed out and a different background).
Basic Styling: The app has a neat, user-friendly layout.
Conclusion
This To-Do List application fulfills all the requirements and offers basic functionality to add, complete, and delete tasks with clean styling.
