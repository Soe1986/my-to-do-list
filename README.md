<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Elegant To-Do List</title>
    <style>
        :root {
            --primary: #6c5ce7;
            --secondary: #a29bfe;
            --accent: #fd79a8;
            --light: #f8
            --dark: #343a40;
            --success: #00b894;
            --warning: #fdcb6e;
            --danger: #d63031;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            padding: 2rem;
            color: var(--dark);
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            padding: 1.5rem 2rem;
            text-align: center;
        }

        .header h1 {
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        .header p {
            opacity: 0.9;
        }

        .todo-app {
            padding: 2rem;
        }

        .input-section {
            display: flex;
            gap: 10px;
            margin-bottom: 2rem;
        }

        .input-section input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #eee;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s;
        }

        .input-section input:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(108, 92, 231, 0.2);
        }

        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }

        .btn-primary {
            background-color: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background-color: #5a4bd6;
            transform: translateY(-2px);
        }

        .btn-secondary {
            background-color: var(--secondary);
            color: white;
        }

        .btn-secondary:hover {
            background-color: #9188fd;
        }

        .btn-danger {
            background-color: var(--danger);
            color: white;
        }

        .btn-danger:hover {
            background-color: #c0392b;
        }

        .filters {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 1.5rem;
        }

        .filter-btn {
            padding: 8px 15px;
            border: none;
            border-radius: 20px;
            background-color: #eee;
            cursor: pointer;
            transition: all 0.3s;
        }

        .filter-btn.active {
            background-color: var(--primary);
            color: white;
        }

        .filter-btn:hover:not(.active) {
            background-color: #ddd;
        }

        .todo-list {
            list-style: none;
        }

        .todo-item {
            display: flex;
            align-items: center;
            padding: 15px;
            margin-bottom: 10px;
            background-color: #f9f9f9;
            border-radius: 8px;
            transition: all 0.3s;
            position: relative;
        }

        .todo-item:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }

        .todo-item.completed {
            background-color: #f0f0f0;
        }

        .todo-item.completed .todo-text {
            text-decoration: line-through;
            color: #888;
        }

        .todo-checkbox {
            margin-right: 15px;
            width: 20px;
            height: 20px;
            cursor: pointer;
        }

        .todo-text {
            flex: 1;
            font-size: 16px;
            word-break: break-word;
        }

        .todo-actions {
            display: flex;
            gap: 10px;
            margin-left: 15px;
        }

        .action-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 16px;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
        }

        .edit-btn {
            color: var(--warning);
        }

        .edit-btn:hover {
            background-color: rgba(253, 203, 110, 0.1);
        }

        .delete-btn {
            color: var(--danger);
        }

        .delete-btn:hover {
            background-color: rgba(214, 48, 49, 0.1);
        }

        .stats {
            margin-top: 2rem;
            padding-top: 1rem;
            border-top: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            color: #666;
            font-size: 14px;
        }

        .empty-state {
            text-align: center;
            padding: 3rem 0;
            color: #888;
        }

        .empty-state img {
            max-width: 200px;
            margin-bottom: 1rem;
            opacity: 0.7;
        }

        .priority-select {
            margin-left: 10px;
            padding: 8px;
            border-radius: 5px;
            border: 1px solid #ddd;
        }

        .priority-high {
            border-left: 4px solid var(--danger);
        }

        .priority-medium {
            border-left: 4px solid var(--warning);
        }

        .priority-low {
            border-left: 4px solid var(--success);
        }

        @media (max-width: 600px) {
            body {
                padding: 1rem;
            }
            
            .input-section {
                flex-direction: column;
            }
            
            .filters {
                flex-wrap: wrap;
            }
            
            .todo-actions {
                margin-left: 5px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>My To-Do List</h1>
            <p>Organize your tasks efficiently</p>
        </div>
        
        <div class="todo-app">
            <div class="input-section">
                <input type="text" id="todo-input" placeholder="Add a new task...">
                <select id="priority-select" class="priority-select">
                    <option value="low">Low Priority</option>
                    <option value="medium">Medium Priority</option>
                    <option value="high">High Priority</option>
                </select>
                <button class="btn btn-primary" id="add-btn">Add Task</button>
            </div>
            
            <div class="filters">
                <button class="filter-btn active" data-filter="all">All</button>
                <button class="filter-btn" data-filter="active">Active</button>
                <button class="filter-btn" data-filter="completed">Completed</button>
            </div>
            
            <ul class="todo-list" id="todo-list">
                <!-- Tasks will be added here dynamically -->
            </ul>
            
            <div class="empty-state" id="empty-state">
                <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJub25lIiBzdHJva2U9ImN1cnJlbnRDb2xvciIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbGluZWNhcD0icm91bmQiIHN0cm9rZS1saW5lam9pbj0icm91bmQiIGNsYXNzPSJsdWNpZGUgbHVjaWRlLWxpc3QtY2hlY2siPjxwYXRoIGQ9Im0zIDE3IDIgMiA0LTQiLz48cGF0aCBkPSJNMyA3IDIgOGw0IDQiLz48cGF0aCBkPSJNMyAxMiAyIDEzbDQgNCIvPjxwYXRoIGQ9Ik0xMSAxN2gxMCIvPjxwYXRoIGQ9Ik0xMSA3aDEwIi8+PHBhdGggZD0iTTExIDEyaDEwIi8+PC9zdmc+" alt="No tasks">
                <h3>No tasks yet</h3>
                <p>Add your first task to get started!</p>
            </div>
            
            <div class="stats" id="stats">
                <span id="total-count">0 tasks</span>
                <span id="completed-count">0 completed</span>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const todoInput = document.getElementById('todo-input');
            const prioritySelect = document.getElementById('priority-select');
            const addBtn = document.getElementById('add-btn');
            const todoList = document.getElementById('todo-list');
            const emptyState = document.getElementById('empty-state');
            const stats = document.getElementById('stats');
            const totalCount = document.getElementById('total-count');
            const completedCount = document.getElementById('completed-count');
            const filterBtns = document.querySelectorAll('.filter-btn');
            
            // State
            let todos = JSON.parse(localStorage.getItem('todos')) || [];
            let currentFilter = 'all';
            
            // Initialize
            renderTodos();
            updateStats();
            
            // Event Listeners
            addBtn.addEventListener('click', addTodo);
            todoInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') addTodo();
            });
            
            filterBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    filterBtns.forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    currentFilter = this.dataset.filter;
                    renderTodos();
                });
            });
            
            // Functions
            function addTodo() {
                const text = todoInput.value.trim();
                const priority = prioritySelect.value;
                
                if (text) {
                    const newTodo = {
                        id: Date.now(),
                        text,
                        completed: false,
                        priority,
                        createdAt: new Date().toISOString()
                    };
                    
                    todos.unshift(newTodo);
                    saveTodos();
                    renderTodos();
                    updateStats();
                    
                    todoInput.value = '';
                    todoInput.focus();
                }
            }
            
            function renderTodos() {
                // Filter todos based on current filter
                let filteredTodos = [];
                
                switch (currentFilter) {
                    case 'active':
                        filteredTodos = todos.filter(todo => !todo.completed);
                        break;
                    case 'completed':
                        filteredTodos = todos.filter(todo => todo.completed);
                        break;
                    default:
                        filteredTodos = [...todos];
                }
                
                // Render todos
                if (filteredTodos.length === 0) {
                    emptyState.style.display = 'block';
                    todoList.style.display = 'none';
                } else {
                    emptyState.style.display = 'none';
                    todoList.style.display = 'block';
                    
                    todoList.innerHTML = filteredTodos.map(todo => `
                        <li class="todo-item ${todo.completed ? 'completed' : ''} priority-${todo.priority}" data-id="${todo.id}">
                            <input type="checkbox" class="todo-checkbox" ${todo.completed ? 'checked' : ''}>
                            <span class="todo-text">${todo.text}</span>
                            <div class="todo-actions">
                                <button class="action-btn edit-btn" title="Edit">✏️</button>
                                <button class="action-btn delete-btn" title="Delete">🗑️</button>
                            </div>
                        </li>
                    `).join('');
                    
                    // Add event listeners to the new elements
                    document.querySelectorAll('.todo-checkbox').forEach(checkbox => {
                        checkbox.addEventListener('change', toggleTodo);
                    });
                    
                    document.querySelectorAll('.edit-btn').forEach(btn => {
                        btn.addEventListener('click', editTodo);
                    });
                    
                    document.querySelectorAll('.delete-btn').forEach(btn => {
                        btn.addEventListener('click', deleteTodo);
                    });
                }
            }
            
            function toggleTodo(e) {
                const id = parseInt(e.target.closest('.todo-item').dataset.id);
                const todo = todos.find(t => t.id === id);
                
                if (todo) {
                    todo.completed = e.target.checked;
                    saveTodos();
                    renderTodos();
                    updateStats();
                }
            }
            
            function editTodo(e) {
                const item = e.target.closest('.todo-item');
                const id = parseInt(item.dataset.id);
                const todo = todos.find(t => t.id === id);
                
                if (!todo) return;
                
                const textElement = item.querySelector('.todo-text');
                const currentText = todo.text;
                
                // Create input field
                const input = document.createElement('input');
                input.type = 'text';
                input.value = currentText;
                input.className = 'edit-input';
                input.style.flex = '1';
                input.style.padding = '5px';
                input.style.border = '1px solid #ddd';
                input.style.borderRadius = '4px';
                
                // Replace text with input field
                textElement.replaceWith(input);
                input.focus();
                
                // Save function
                const saveEdit = () => {
                    const newText = input.value.trim();
                    if (newText && newText !== currentText) {
                        todo.text = newText;
                        saveTodos();
                    }
                    renderTodos();
                };
                
                // Event listeners
                input.addEventListener('blur', saveEdit);
                input.addEventListener('keypress', (e) => {
                    if (e.key === 'Enter') saveEdit();
                });
            }
            
            function deleteTodo(e) {
                const id = parseInt(e.target.closest('.todo-item').dataset.id);
                todos = todos.filter(todo => todo.id !== id);
                saveTodos();
                renderTodos();
                updateStats();
            }
            
            function saveTodos() {
                localStorage.setItem('todos', JSON.stringify(todos));
            }
            
            function updateStats() {
                const total = todos.length;
                const completed = todos.filter(todo => todo.completed).length;
                
                totalCount.textContent = `${total} ${total === 1 ? 'task' : 'tasks'}`;
                completedCount.textContent = `${completed} completed`;
            }
        });
    </script>
</body>
</html>
