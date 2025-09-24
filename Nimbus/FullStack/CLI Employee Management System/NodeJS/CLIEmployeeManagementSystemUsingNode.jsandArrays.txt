// Import the built-in 'readline' module to handle user input from the command line.
const readline = require('readline');

// Create an interface for reading from standard input (keyboard) and writing to standard output (console).
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

// Use an array to store employee data in memory.
// Each employee is an object with a 'name' and 'id'.
let employees = [
    { name: 'Alice', id: 'E101' },
    { name: 'Bob', id: 'E102' },
    { name: 'Charlie', id: 'E103' }
];

/**
 * Displays the main menu and prompts the user for a choice.
 */
function showMenu() {
  console.log('\nEmployee Management System');
  console.log('1. Add Employee');
  console.log('2. List Employees');
  console.log('3. Remove Employee');
  console.log('4. Exit');

  // Ask the user for their choice and process it in the callback function.
  rl.question('\nEnter your choice: ', (choice) => {
    switch (choice.trim()) {
      case '1':
        addEmployee();
        break;
      case '2':
        listEmployees();
        break;
      case '3':
        removeEmployee();
        break;
      case '4':
        exitApp();
        break;
      default:
        console.log('Invalid choice. Please enter a number between 1 and 4.');
        showMenu(); // Show the menu again if the choice is invalid.
        break;
    }
  });
}

/**
 * Prompts for new employee details and adds them to the 'employees' array.
 */
function addEmployee() {
  rl.question('Enter employee name: ', (name) => {
    rl.question('Enter employee ID: ', (id) => {
      // Create a new employee object and add it to the array.
      employees.push({ name, id });
      console.log(`Employee ${name} (ID: ${id}) added successfully.`);
      showMenu(); // Go back to the main menu.
    });
  });
}

/**
 * Displays a formatted list of all current employees.
 */
function listEmployees() {
  if (employees.length === 0) {
    console.log('No employees in the list.');
  } else {
    console.log('\nEmployee List:');
    // Loop through the array and print each employee's details.
    employees.forEach((employee, index) => {
      console.log(`${index + 1}. Name: ${employee.name}, ID: ${employee.id}`);
    });
  }
  showMenu(); // Go back to the main menu.
}

/**
 * Prompts for an employee ID and removes the matching employee from the array.
 */
function removeEmployee() {
  rl.question('Enter employee ID to remove: ', (id) => {
    // Find the index of the employee with the given ID.
    const index = employees.findIndex(emp => emp.id === id);

    if (index !== -1) {
      // Use splice() to remove the employee from the array.
      // splice returns an array of removed items; we get the first one.
      const removedEmployee = employees.splice(index, 1);
      console.log(`Employee ${removedEmployee[0].name} (ID: ${removedEmployee[0].id}) removed successfully.`);
    } else {
      console.log(`Employee with ID ${id} not found.`);
    }
    showMenu(); // Go back to the main menu.
  });
}

/**
 * Exits the application.
 */
function exitApp() {
  console.log('Exiting the application. Goodbye! 👋');
  // Close the readline interface, which allows the program to terminate.
  rl.close();
}

// Initial call to start the application by showing the menu.
showMenu();
