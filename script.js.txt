let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

function saveTasks() {
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function addTask() {
  const text = document.getElementById("taskInput").value;
  const date = document.getElementById("deadline").value;
  const priority = document.getElementById("priority").value;

  if (text === "") return;

  const task = {
    text: text,
    date: date,
    priority: priority,
    completed: false
  };

  tasks.push(task);
  saveTasks();
  displayTasks();
}

function displayTasks() {
  const list = document.getElementById("taskList");
  list.innerHTML = "";

  tasks.forEach((task, index) => {
    const li = document.createElement("li");

    li.classList.add(task.priority.toLowerCase());

    if (task.completed) {
      li.classList.add("completed");
    }

    li.innerHTML = `
      <strong>${task.text}</strong><br>
      Deadline: ${task.date} | Priority: ${task.priority}
      <br>
      <button onclick="completeTask(${index})">Complete</button>
      <button onclick="deleteTask(${index})">Delete</button>
    `;

    list.appendChild(li);
  });

  updateProgress();
}

function completeTask(index) {
  tasks[index].completed = !tasks[index].completed;
  saveTasks();
  displayTasks();
}

function deleteTask(index) {
  tasks.splice(index, 1);
  saveTasks();
  displayTasks();
}

function updateProgress() {
  const completed = tasks.filter(task => task.completed).length;
  const total = tasks.length;
  const percent = total === 0 ? 0 : Math.round((completed / total) * 100);
  document.getElementById("progress").innerText = "Progress: " + percent + "%";
}

displayTasks();
const date = document.getElementById("deadline").value;
const time = document.getElementById("deadtime").value;
const deadlineDateTime = new Date(date + "T" + time);
const now = new Date();

if (deadlineDateTime < now && !task.completed) {
    li.style.backgroundColor = "#ffcccc"; // light red
}


