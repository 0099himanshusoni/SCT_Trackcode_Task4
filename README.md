# SCT_Trackcode_Task4

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List App</title>
    <!-- Bootstrap CSS -->
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-color: #f8f9fa;
            color: #343a40;
        }

        .container {
            max-width: 600px;
            margin-top: 50px;
        }

        .task {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border: 1px solid #dee2e6;
            border-radius: 5px;
            margin-bottom: 10px;
            background-color: #ffffff;
        }

        .task.completed {
            text-decoration: line-through;
            background-color: #d4edda;
        }

        .btn-primary {
            background-color: #007bff;
            border-color: #007bff;
        }

        .btn-danger {
            background-color: #dc3545;
            border-color: #dc3545;
        }

        .btn-warning {
            background-color: #ffc107;
            border-color: #ffc107;
        }

        .edit-input {
            display: none;
            flex-grow: 1;
            margin-right: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1 class="text-center">To-Do List</h1>
        <div class="form-group">
            <input type="text" id="taskInput" class="form-control" placeholder="Add a new task..." />
            <input type="datetime-local" id="dueDateInput" class="form-control mt-2" placeholder="Set due date..." />
            <button id="addTaskBtn" class="btn btn-primary mt-2">Add Task</button>
        </div>

        <div id="taskList"></div>
    </div>

    <!-- Bootstrap JS and jQuery -->
    <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.2/dist/js/bootstrap.bundle.min.js"></script>

    <script>
        const taskList = document.getElementById('taskList');
        const taskInput = document.getElementById('taskInput');
        const dueDateInput = document.getElementById('dueDateInput');
        const addTaskBtn = document.getElementById('addTaskBtn');

        addTaskBtn.addEventListener('click', addTask);

        function addTask() {
            const taskText = taskInput.value.trim();
            const dueDate = dueDateInput.value;

            if (taskText === '') {
                alert('Please enter a task.');
                return;
            }

            const taskElement = createTaskElement(taskText, dueDate);
            taskList.appendChild(taskElement);
            taskInput.value = '';
            dueDateInput.value = '';
        }

        function createTaskElement(taskText, dueDate) {
            const taskDiv = document.createElement('div');
            taskDiv.className = 'task';

            const taskContent = document.createElement('span');
            taskContent.textContent = taskText;

            if (dueDate) {
                const dateSpan = document.createElement('span');
                dateSpan.className = 'badge badge-info ml-2';
                dateSpan.textContent = new Date(dueDate).toLocaleString();
                taskDiv.appendChild(dateSpan);
            }

            const editInput = document.createElement('input');
            editInput.type = 'text';
            editInput.className = 'edit-input form-control';
            editInput.value = taskText;

            const editBtn = document.createElement('button');
            editBtn.className = 'btn btn-warning btn-sm';
            editBtn.textContent = 'Edit';
            editBtn.onclick = () => {
                if (editInput.style.display === 'none') {
                    editInput.style.display = 'inline';
                    editBtn.textContent = 'Save';
                } else {
                    taskContent.textContent = editInput.value;
                    editInput.style.display = 'none';
                    editBtn.textContent = 'Edit';
                }
            };

            const completeBtn = document.createElement('button');
            completeBtn.className = 'btn btn-success btn-sm';
            completeBtn.textContent = 'Complete';
            completeBtn.onclick = () => {
                taskDiv.classList.toggle('completed');
            };

            const deleteBtn = document.createElement('button');
            deleteBtn.className = 'btn btn-danger btn-sm';
            deleteBtn.textContent = 'Delete';
            deleteBtn.onclick = () => {
                taskDiv.remove();
            };

            taskDiv.appendChild(taskContent);
            taskDiv.appendChild(editInput);
            taskDiv.appendChild(editBtn);
            taskDiv.appendChild(completeBtn);
            taskDiv.appendChild(deleteBtn);

            return taskDiv;
        }
    </script>
</body>
</html>
