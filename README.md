# MWAD-EX_03-To-Do-List-using-JavaScript
### Name:Swetha D
### Reg no:212223040222
## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
```

<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Todo Application</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #8b33dd; 
            text-align: center;
        }
        header, footer {
            background-color: rgb(68, 167, 187); 
            color: rgb(255, 255, 255);
            padding: 15px;
            font-size: 20px;
            font-weight: bold;
        }
        .todo-container {
            max-width: 400px;
            background: rgb(0, 105, 128);
            margin: 30px auto;
            padding: 90px;
            border-radius: 100px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border: 2px solid #64f6b9;
        }
        .input-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
        }
        .todo-input, .todo-date, .submit-btn {
            width: 90%;
            padding: 10px;
            border: 2px solid #64f6e5;
            border-radius: 4px;
            text-align: center;
        }
        .submit-btn {
            background-color: #64e3f6;
            color: rgb(9, 2, 2);
            font-size: 16px;
            cursor: pointer;
            border: none;
            transition: 0.3s;
        }
        .submit-btn:hover {
            background-color: #42a5f5;
        }
        .todo-list {
            list-style: none;
            padding: 0;
        }
        .todo-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 10px;
            margin-bottom: 5px;
            background-color: #b3e5fc; 
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        .todo-item.completed span {
            text-decoration: line-through;
            color: gray;
        }
        .todo-buttons {
            display: flex;
            gap: 5px;
            margin-top: 5px;
        }
        .todo-buttons button {
            padding: 5px 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .complete-btn {
            background-color: #81c784; 
            color: white;
        }
        .delete-btn {
            background-color: #e57373; 
            color: white;
        }
        .task-date {
            font-size: 12px;
            color: #555;
            margin-top: 5px;
        }
        
        .popup {
            visibility: hidden;
            min-width: 250px;
            background-color: #4caf50;
            color: white;
            text-align: center;
            border-radius: 8px;
            padding: 10px;
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            opacity: 0;
            transition: opacity 0.5s ease-in-out;
        }
        .popup.show {
            visibility: visible;
            opacity: 1;
        }
    </style>
</head>
<body>
    <header>My Todo Application</header>
    <div class="todo-container">
        <h2>My To-Do List</h2>
        <div class="input-container">
            <input type="text" id="todo-input" class="todo-input" placeholder="Add a new task">
            <input type="date" id="todo-date" class="todo-date">
            <button id="submit-btn" class="submit-btn">Submit</button>
        </div>
        <ul id="todo-list" class="todo-list"></ul>
    </div>
    <footer>&copy; 2025 @ Swetha D| All rights reserved.</footer>

    <!-- Pop-up Notification -->
    <div id="popup" class="popup"></div>

    <script>
        const todoInput = document.getElementById('todo-input');
        const todoDate = document.getElementById('todo-date');
        const submitBtn = document.getElementById('submit-btn');
        const todoList = document.getElementById('todo-list');
        const popup = document.getElementById('popup');

        function showPopup(message) {
            popup.textContent = message;
            popup.classList.add('show');
            setTimeout(() => {
                popup.classList.remove('show');
            }, 2000); // Pop-up disappears after 2 seconds
        }

        function addTodo() {
            const task = todoInput.value.trim();
            const date = todoDate.value;

            if (task === '' || date === '') {
                showPopup("⚠️ Enter a task & date!");
                return;
            }

            const li = document.createElement('li');
            li.className = 'todo-item';

            const span = document.createElement('span');
            span.textContent = task;

            const dateSpan = document.createElement('span');
            dateSpan.className = 'task-date';
            dateSpan.textContent = `📅 ${date}`;

            const buttonsDiv = document.createElement('div');
            buttonsDiv.className = 'todo-buttons';

            const completeBtn = document.createElement('button');
            completeBtn.textContent = '✔';
            completeBtn.className = 'complete-btn';
            completeBtn.onclick = () => {
                li.classList.toggle('completed');
            };

            const deleteBtn = document.createElement('button');
            deleteBtn.textContent = '✖';
            deleteBtn.className = 'delete-btn';
            deleteBtn.onclick = () => {
                todoList.removeChild(li);
            };

            buttonsDiv.appendChild(completeBtn);
            buttonsDiv.appendChild(deleteBtn);

            li.appendChild(span);
            li.appendChild(dateSpan);
            li.appendChild(buttonsDiv);

            todoList.appendChild(li);

            // Show compact pop-up notification
            showPopup(`✅ Task Added: "${task}"`);

            // Clear inputs
            todoInput.value = '';
            todoDate.value = '';
        }

        submitBtn.addEventListener('click', addTodo);
        todoInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') addTodo();
        });
        todoDate.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') addTodo();
        });
    </script>
</body>
</html>
```

## OUTPUT
![{8F2224AE-5030-4387-9857-9EBC370CC660}](https://github.com/user-attachments/assets/c97a3f77-6207-4a5b-86f2-cccdc1e234bd)

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
