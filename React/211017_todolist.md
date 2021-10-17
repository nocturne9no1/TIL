# React 로 todo list 만들기

```react
import { useState } from "react";

export default function App() {
  const [ todo, setTodo ] = useState("");
  const [ todoList, setTodoList ] = useState([]);

  const handleSubmit = (event) => {
    event.preventDefault()
    setTodoList([...todoList, todo])
  }

  const handleTodoChange = (event) => {
    setTodo(event.target.value)
  }

  const deleteTodo = idx => {
    setTodoList(todoList.filter((todo, index) => index !== idx))
  }
 
  return (
    <div>
      <form>
        <input onChange={handleTodoChange} type="text" />
        <button onClick={handleSubmit} type="submit">ADD</button>
      </form>
      { todoList.map((todo, idx) => (
        <div key={idx}>
          <span>{todo}</span>
          <button onClick={() => deleteTodo(idx)}>X</button>
        </div>
      ))}
    </div>
  );
}
```

