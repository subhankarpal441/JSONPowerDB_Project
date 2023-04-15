# JSONPowerDB_Project
The micro Project Topic is  :  Project Management Form that will store data in PROJECT-TABLE relation of COLLEGE-DB database, Input Fields: {Project-ID, Project-Name, Assigned-To, Assignment-Date, Deadline}, Primary key: Project ID


<form id="project-form">
  <label for="project-id">Project ID:</label>
  <input type="text" id="project-id" name="project-id" required>

  <label for="project-name">Project Name:</label>
  <input type="text" id="project-name" name="project-name" disabled>

  <label for="assigned-to">Assigned To:</label>
  <input type="text" id="assigned-to" name="assigned-to" disabled>

  <label for="assignment-date">Assignment Date:</label>
  <input type="date" id="assignment-date" name="assignment-date" disabled>

  <label for="deadline">Deadline:</label>
  <input type="date" id="deadline" name="deadline" disabled>

  <button type="submit" id="save-btn" disabled>Save</button>
  <button type="button" id="update-btn" disabled>Update</button>
  <button type="reset" id="reset-btn" disabled>Reset</button>
</form>


In this code, the form has an ID of "project-form" and includes input fields for each of the specified input fields in the micro project topic. The "Project ID" input field is required and serves as the primary key. All other input fields and buttons are initially disabled.

We can use JavaScript to implement the behavior of the form buttons, such as enabling or disabling fields and buttons, checking for valid data, and saving or updating data in the database. Here's an example JavaScript code:

// Get references to the form and its input fields and buttons
const form = document.getElementById("project-form");
const projectIdInput = document.getElementById("project-id");
const projectNameInput = document.getElementById("project-name");
const assignedToInput = document.getElementById("assigned-to");
const assignmentDateInput = document.getElementById("assignment-date");
const deadlineInput = document.getElementById("deadline");
const saveBtn = document.getElementById("save-btn");
const updateBtn = document.getElementById("update-btn");
const resetBtn = document.getElementById("reset-btn");

// Disable all input fields and buttons except for Project ID
projectNameInput.disabled = true;
assignedToInput.disabled = true;
assignmentDateInput.disabled = true;
deadlineInput.disabled = true;
saveBtn.disabled = true;
updateBtn.disabled = true;
resetBtn.disabled = true;

// Set focus on the first input field (Project ID)
projectIdInput.focus();

// Event listener for form submission
form.addEventListener("submit", function(event) {
  event.preventDefault(); // Prevent default form submission behavior

  // Check that all input fields are filled in
  if (projectIdInput.value && projectNameInput.value && assignedToInput.value && assignmentDateInput.value && deadlineInput.value) {
    // Save data to the database and reset the form
    saveDataToDatabase();
    resetForm();
  } else {
    alert("Please fill in all fields.");
  }
});

// Event listener for Project ID input field change
projectIdInput.addEventListener("change", function() {
  const projectId = projectIdInput.value;
  const projectData = getDataFromDatabase(projectId);

  if (projectData) {
    // Display existing project data in the form
    projectNameInput.value = projectData.projectName;
    assignedToInput.value = projectData.assignedTo;
    assignmentDateInput.value = projectData.assignmentDate;
    deadlineInput.value = projectData.deadline;

    // Enable Update and Reset buttons, and disable Project ID field
    projectIdInput.disabled = true;
    projectNameInput.disabled = false;
    assignedToInput.disabled = false;
    assignmentDateInput.disabled = false;
    deadlineInput.disabled = false;
    saveBtn.addEventListener('click', saveProjectData);
    updateBtn.addEventListener('click', updateProjectData);
    resetBtn.addEventListener('click', initForm);
