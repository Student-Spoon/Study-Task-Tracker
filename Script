/* ============================================

   STUDY TASK TRACKER — JAVASCRIPT

   Handles page navigation, local storage,

   saving, displaying, and deleting tasks.

============================================ */

// Local storage key — used to save/retrieve task data

const STORAGE_KEY = "studyTasks";

/* ===== PAGE NAVIGATION ===== */

// Switches between pages by showing/hiding sections

function showPage(pageId) {

  // Hide all pages

  document.querySelectorAll(".page").forEach(page => {

    page.classList.remove("active");

  });

  // Show selected page

  document.getElementById(pageId).classList.add("active");

  // Close mobile menu after navigating

  document.getElementById("navMenu").classList.remove("show");

  // If user navigates to Saved Tasks, refresh the list

  if (pageId === "savedTasks") {

    displayTasks();

  }

}

/* ===== MOBILE MENU TOGGLE ===== */

function toggleMenu() {

  document.getElementById("navMenu").classList.toggle("show");

}

/* ===== SAVE TASK TO LOCAL STORAGE ===== */

function saveTask(event) {

  event.preventDefault(); // Prevent form from refreshing the page

  // Get values from form inputs

  const title = document.getElementById("taskTitle").value.trim();

  const subject = document.getElementById("taskSubject").value.trim();

  const dueDate = document.getElementById("taskDate").value;

  const priority = document.getElementById("taskPriority").value;

  const notes = document.getElementById("taskNotes").value.trim();

  const message = document.getElementById("saveMessage");

  // Basic validation — check required fields

  if (title === "" || subject === "" || dueDate === "" || priority === "") {

    message.textContent = "Please complete all required fields.";

    message.classList.add("error");

    return;

  }

  // Create a new task object

  const newTask = {

    title: title,

    subject: subject,

    dueDate: dueDate,

    priority: priority,

    notes: notes

  };

  // Get existing tasks from local storage (or start with empty array)

  let tasks = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];

  // Add new task to the array

  tasks.push(newTask);

  // Save updated array back to local storage as a JSON string

  localStorage.setItem(STORAGE_KEY, JSON.stringify(tasks));

  // Show success message

  message.textContent = "✅ Task saved successfully!";

  message.classList.remove("error");

  // Reset the form

  event.target.reset();

  // Clear message after 3 seconds

  setTimeout(() => {

    message.textContent = "";

  }, 3000);

}

/* ===== DISPLAY SAVED TASKS ===== */

function displayTasks() {

  const taskList = document.getElementById("taskList");

  // Get tasks from local storage

  const tasks = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];

  // Clear current display

  taskList.innerHTML = "";

  // Show message if no tasks saved

  if (tasks.length === 0) {

    taskList.innerHTML = `
<div class="empty-message">

        No tasks saved yet. Add your first task to get started!
</div>

    `;

    return;

  }

  // Loop through each task and create a card

  tasks.forEach((task, index) => {

    // Determine priority colour class

    const priorityClass = "priority-" + task.priority.toLowerCase();

    // Format date for display

    const formattedDate = task.dueDate ? formatDate(task.dueDate) : "No date set";

    // Build the task card HTML

    taskList.innerHTML += `
<div class="task-card">
<span class="priority-badge ${priorityClass}">${task.priority}</span>
<h3>${task.title}</h3>
<p>📚 ${task.subject}</p>
<p>📅 Due: ${formattedDate}</p>
<p class="notes">${task.notes || "No additional notes."}</p>
<button class="delete-btn" onclick="deleteTask(${index})">Delete</button>
</div>

    `;

  });

}

/* ===== DELETE INDIVIDUAL TASK ===== */

function deleteTask(index) {

  // Confirm before deleting

  const confirmDelete = confirm("Are you sure you want to delete this task?");

  if (!confirmDelete) return;

  // Get tasks from local storage

  let tasks = JSON.parse(localStorage.getItem(STORAGE_KEY)) || [];

  // Remove the task at the given index

  tasks.splice(index, 1);

  // Save updated array back to local storage

  localStorage.setItem(STORAGE_KEY, JSON.stringify(tasks));

  // Refresh the displayed list

  displayTasks();

}

/* ===== CLEAR ALL TASKS ===== */

function clearAllTasks() {

  // Confirm before clearing

  const confirmClear = confirm("Are you sure you want to delete ALL saved tasks? This cannot be undone.");

  if (!confirmClear) return;

  // Remove the storage key entirely

  localStorage.removeItem(STORAGE_KEY);

  // Refresh display

  displayTasks();

}

/* ===== FORMAT DATE (helper function) ===== */

// Converts "2026-07-05" into "5 July 2026"

function formatDate(dateString) {

  const date = new Date(dateString);

  const options = { day: "numeric", month: "long", year: "numeric" };

  return date.toLocaleDateString("en-GB", options);

}

/* ===== INITIAL LOAD ===== */

// Display tasks when page first loads

displayTasks();
