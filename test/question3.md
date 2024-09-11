### Problem Statement: 

You are building a **task manager** for users to track their daily tasks. Implement a function `taskManager` that takes no parameters and returns an object with the following methods:

1. **addTask(task)**: Adds a new task (string) to the user's task list.
2. **removeTask(task)**: Removes the specified task from the task list if it exists. If the task does not exist, return the message `"Task not found"`.
3. **listTasks()**: Returns an array of all tasks currently in the task list.

The list of tasks should be private and only accessible through the provided methods. Ensure that tasks cannot be directly accessed or modified outside the methods.

### Requirements:
- The `taskManager` function should allow users to manage their tasks only via the provided methods.
- The task list should remain private, and the tasks should not be accessible directly.
- When removing a task, check if it exists. If not, return `"Task not found"`.

### Hints:
- Use closures to keep the task list private, ensuring that tasks are only added, removed, or viewed using the defined methods.
- You may want to use an array to store the tasks and provide methods to add, remove, and list tasks.

### Example:

```javascript
const myTasks = taskManager();
myTasks.addTask('Do laundry');
myTasks.addTask('Buy groceries');
myTasks.listTasks();                // Returns: ['Do laundry', 'Buy groceries']
myTasks.removeTask('Go jogging');   // Returns: "Task not found"
myTasks.removeTask('Buy groceries'); 
myTasks.listTasks();                // Returns: ['Do laundry']
```

### Code Stub (For Students to Work On):

```javascript
function taskManager() {
  // Students will implement the function here
}
```

### Solution Approach:

1. **Use Closures:** 
   - Keep the task list private within the scope of the `taskManager` function using closures.
   - Define methods `addTask`, `removeTask`, and `listTasks` to manage the task list.

2. **addTask Method:**
   - This method will append the task to the private array storing the tasks.

3. **removeTask Method:**
   - This method will check if the specified task exists in the list. If it does, remove it from the array. If it doesn’t, return `"Task not found"`.

4. **listTasks Method:**
   - Return the entire task list as an array.

### Complete Solution:

```javascript
function taskManager() {
  let tasks = [];

  return {
    addTask: function(task) {
      tasks.push(task);
    },
    removeTask: function(task) {
      const index = tasks.indexOf(task);
      if (index === -1) {
        return "Task not found";
      }
      tasks.splice(index, 1);
    },
    listTasks: function() {
      return tasks;
    }
  };
}
```

### Test Cases:

```javascript
// Test Case 1: Basic functionality
const myTasks = taskManager();
myTasks.addTask('Do laundry');
myTasks.addTask('Buy groceries');
console.log(myTasks.listTasks());                 // Output: ['Do laundry', 'Buy groceries']
console.log(myTasks.removeTask('Go jogging'));    // Output: "Task not found"
myTasks.removeTask('Buy groceries');
console.log(myTasks.listTasks());                 // Output: ['Do laundry']

// Test Case 2: Removing non-existing task
const tasks2 = taskManager();
tasks2.addTask('Write code');
console.log(tasks2.removeTask('Test code'));      // Output: "Task not found"
console.log(tasks2.listTasks());                  // Output: ['Write code']

// Test Case 3: Adding and removing tasks
const tasks3 = taskManager();
tasks3.addTask('Do dishes');
tasks3.addTask('Clean room');
tasks3.addTask('Pay bills');
console.log(tasks3.listTasks());                  // Output: ['Do dishes', 'Clean room', 'Pay bills']
tasks3.removeTask('Clean room');
console.log(tasks3.listTasks());                  // Output: ['Do dishes', 'Pay bills']
```

### Explanation:
- The tasks are stored in a private array, `tasks`, within the closure of the `taskManager` function.
- The methods `addTask`, `removeTask`, and `listTasks` allow controlled access and modification of the task list.
- The task list is not accessible directly from outside the function, ensuring privacy through closures.