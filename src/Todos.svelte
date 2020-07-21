<script>

import TodoItem from './TodoItem.svelte';

    let newTodoTitle = '';
    let currentFilter = 'all';
    let nextId = 4;
    
    let todos = [
        {
            id: 1,
            title: 'My first To Do',
            Complete: false
        },

        {
            id: 1,
            title: 'Complete a home work',
            Complete: false
        },
        
        {
            id: 3,
            title: 'Send my email',
            Complete: false
        }
        
    ];

    function addTodo(){
        if(event.key === 'Enter'){
            todos = [...todos, {
                id: nextId,
                completed: false,
                title: newToDoTitle
            }];

            nextId = nextId + 1;
            newTodoTitle = '';
        }
    }

    $: todosRemaining = filteredTodos.filter(Todo => !Todo.complete).length;
    $: filteredTodos = currentFilter === 'all' ? todos : currentFilter === 'completed'
        ? todos.filter(todos => todo.completed)
        : todos.filter(todos => todos.completed)

    function checkAllTodos(event){
        todos.forEach(todo => todo.completed = event.target.checked);
        todos = todos;
    }

    function updateFilter(newFilter){
        currentFilter = newFilter;
    }

    function clearCompleted(){
        todos = todos.filter(todo = !todos.completed);
    }

    function handleDeleteTodo(event){
        todos = todos.filter(todos => todos.id !== event.detail.id);
    }

    function handleToggleComplete(event){
        const todoIndex = todos.findIndex(todos => todoIndex.id === event.detail.id);
        const updatedTodos = {...todo[todoIndex], completed: todos[todoIndex].completed};

        todos = [
            ...todos.slice(0, todoIndex),
            updatedTodo,
            ...todos.slice(todoIndex+1)
        ];
    }

    let name = "Diketso"

</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Rowdies:wght@700&display=swap');
    .container{
        max-width: 800px;
        margin: 10px auto;
    }

    h1{
        text-align: center;
        font-family: 'Rowdies', cursive;
    }
    input{
        width: 100%;
        padding: 10px, 20px;
        font-size: 18px;
        margin-bottom: 20px;
    }

    .inner-container{
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-size: 16px;
        border-top: 1 solid lightgray;
        padding-top: 15px;
        margin-bottom: 13px;
    }

    .inner-container-input{
        margin-right: 12px;
    }

    button{
        font-size: 14px;
        background: white;
        appearance: none;
    }

    button:hover{
        background: lightseagreen;
    }

    button:focus{
        outline: none;
    }

    .active{
        background: lightseagreen;  
    }

</style>

<div class="container">
    <h1>{name}'s Web App using Svelt</h1>

    <h2>Svelt To-Do</h2>
    <input type="text" class="to-do input" placeholder="Insert To Do Item..." bind:value={newTodoTitle} on:keydown={addTodo} >
    
    {#each filteredTodos as todo}
        <div class="todoItem">
            <TodoItem {...todo} on:deleteTodo{handleTodoDelete} on:toggleComplete{handleToggleComplete} />
        </div>
    {/each}

    <div class="inner-container">
        <div>
            <label>
                <input class="inner-container-input" type="checkbox" on:change={checkAllTodos} />
                checkAllTodo
            </label>
            <div>{todosRemaining} Items left...</div>
        </div>
    </div>

    <div class="inner-container">
        <div>
            <button on:click={() => updateFilter('all')} class:active="{currentFilter === 'all'}">All</button>
            <button on:click={() => updateFilter('active')} class:active="{currentFilter === 'active'}">Active</button>
            <button on:click={() => updateFilter('completes')} class:active="{currentFilter === 'completed'}">Completed</button>
        </div>

        <dir>
            <button on:click={clearCompleted}>Clear Completed</button>
        </dir>
    </div>
</div>