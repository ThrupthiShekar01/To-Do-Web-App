# To-Do-Web-App
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do Web App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #1f1f2e;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }

    .todo-container {
      background: #2a2a40;
      padding: 25px;
      border-radius: 12px;
      width: 400px;
      box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.3);
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
    }

    .input-group {
      display: flex;
      gap: 5px;
      margin-bottom: 15px;
    }

    input, button {
      padding: 10px;
      border: none;
      border-radius: 6px;
    }

    input[type="text"], input[type="datetime-local"] {
      flex: 1;
    }

    button {
      background: #4CAF50;
      color: white;
      cursor: pointer;
    }

    button:hover {
      background: #45a049;
    }

    ul {
      list-style: none;
      padding: 0;
    }

    li {
      background: #3c3c5c;
      margin: 8px 0;
      padding: 10px;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    li.completed {
      text-decoration: line-through;
      color: #aaa;
    }

    .actions button {
      margin-left: 5px;
      padding: 5px 8px;
      font-size: 12px;
    }
  </style>
</head>
<body>
  <div class="todo-container">
    <h2>📝 To-Do List</h2>
    <div class="input-group">
      <input type="text" id="taskInput" placeholder="Enter task...">
      <input type="datetime-local" id="taskDateTime">
      <button onclick="addTask()">Add</button>
    </div>
    <ul id="taskList"></ul>
  </div>

  <script>
    function addTask() {
      const taskInput = document.getElementById("taskInput");
      const dateTimeInput = document.getElementById("taskDateTime");
      const taskText = taskInput.value.trim();
      const taskDateTime = dateTimeInput.value;

      if (taskText === "") {
        alert("Please enter a task!");
        return;
      }

      const li = document.createElement("li");
      li.innerHTML = `
        <span>${taskText} <br><small>${taskDateTime ? "⏰ " + taskDateTime : ""}</small></span>
        <div class="actions">
          <button onclick="completeTask(this)">✔</button>
          <button onclick="editTask(this)">✏</button>
          <button onclick="deleteTask(this)">🗑</button>
        </div>
      `;

      document.getElementById("taskList").appendChild(li);
      taskInput.value = "";
      dateTimeInput.value = "";
    }

    function completeTask(button) {
      const li = button.parentElement.parentElement;
      li.classList.toggle("completed");
    }

    function editTask(button) {
      const li = button.parentElement.parentElement;
      const taskText = li.querySelector("span").innerText.split("\n")[0];
      const newTask = prompt("Edit your task:", taskText);
      if (newTask) {
        li.querySelector("span").innerHTML = newTask;
      }
    }

    function deleteTask(button) {
      const li = button.parentElement.parentElement;
      li.remove();
    }
  </script>
</body>
</html>
