// TodoApp.js

import React, { useState } from 'react';

/**
 * A simple Todo List application component.
 * It allows users to add new tasks and remove existing ones.
 */
function TodoApp() {
  // 1. State for the list of tasks. Each task is an object with an id and text.
  const [tasks, setTasks] = useState([]);
  
  // 2. State for the current input field value.
  const [inputValue, setInputValue] = useState('');

  /**
   * Handles adding a new task to the list.
   */
  const handleAddTask = () => {
    // Check if the input is not empty or just whitespace
    if (inputValue.trim() === '') {
      alert('Task cannot be empty!');
      return;
    }

    // Create a new task object
    const newTask = {
      // Use Date.now() for a simple, unique ID (better to use a proper library like uuid in production)
      id: Date.now(), 
      text: inputValue.trim(),
    };

    // Add the new task to the tasks array
    setTasks([...tasks, newTask]);

    // Clear the input field after adding the task
    setInputValue('');
  };

  /**
   * Handles removing a task from the list based on its id.
   * @param {number} id - The unique identifier of the task to remove.
   */
  const handleRemoveTask = (id) => {
    // Filter out the task with the matching id
    const updatedTasks = tasks.filter(task => task.id !== id);
    setTasks(updatedTasks);
  };

  return (
    <div style={{ padding: '20px', maxWidth: '400px', margin: 'auto', fontFamily: 'Arial, sans-serif' }}>
      <h1>Simple Todo App 📝</h1>
      
      {/* Input Field and "Add" Button 
      */}
      <div style={{ marginBottom: '20px', display: 'flex' }}>
        <input
          type="text"
          value={inputValue}
          // Update the inputValue state as the user types
          onChange={(e) => setInputValue(e.target.value)}
          // Allow adding a task by pressing the 'Enter' key
          onKeyPress={(e) => {
            if (e.key === 'Enter') {
              handleAddTask();
            }
          }}
          placeholder="Enter a new task..."
          style={{ flexGrow: 1, padding: '10px', fontSize: '16px', border: '1px solid #ccc', borderRadius: '4px 0 0 4px' }}
        />
        <button
          onClick={handleAddTask}
          style={{ 
            padding: '10px 15px', 
            fontSize: '16px', 
            backgroundColor: '#007bff', 
            color: 'white', 
            border: 'none', 
            borderRadius: '0 4px 4px 0', 
            cursor: 'pointer' 
          }}
        >
          Add
        </button>
      </div>

      {/* Render List using map() 
      */}
      {tasks.length === 0 ? (
        <p style={{ textAlign: 'center', color: '#666' }}>No tasks yet! Start adding some. 🎉</p>
      ) : (
        <ul style={{ listStyle: 'none', padding: 0 }}>
          {tasks.map((task) => (
            <li 
              key={task.id} 
              style={{ 
                display: 'flex', 
                justifyContent: 'space-between', 
                alignItems: 'center', 
                padding: '10px', 
                marginBottom: '8px', 
                backgroundColor: '#f9f9f9', 
                border: '1px solid #eee', 
                borderRadius: '4px' 
              }}
            >
              <span style={{ flexGrow: 1 }}>{task.text}</span>
              <button
                // Call the remove handler with the task's ID
                onClick={() => handleRemoveTask(task.id)}
                style={{ 
                  marginLeft: '10px', 
                  padding: '5px 10px', 
                  backgroundColor: '#dc3545', 
                  color: 'white', 
                  border: 'none', 
                  borderRadius: '4px', 
                  cursor: 'pointer' 
                }}
              >
                Remove
              </button>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

export default TodoApp;
