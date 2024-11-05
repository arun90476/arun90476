<!-- Spinner for loading -->
<div id="loadingSpinner"></div>

/* Styling for the spinner */
#loadingSpinner {
    display: none;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border: 4px solid #f3f3f3;
    border-top: 4px solid #3498db;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}



// Function to show the spinner
function showLoadingSpinner() {
    document.getElementById("loadingSpinner").style.display = 'block'; // Show the spinner
}

// Function to hide the spinner
function hideLoadingSpinner() {
    document.getElementById("loadingSpinner").style.display = 'none'; // Hide the spinner
}



// Submit Form with loading spinner
function submitForm(event) {
    // Prevent the form from submitting immediately
    event.preventDefault();

    var accountNumber = document.getElementById("accountNumber").value;
    var product = document.getElementById("secondDropdown").value;

    // Show the spinner before submitting the form
    showLoadingSpinner();

    // Validation logic
    if (accountNumber.trim() === "" && (product === "" || product === "Select")) {
        // Show error alert
        document.getElementById("errorAlert").style.display = 'block';
        hideLoadingSpinner(); // Hide the spinner if validation fails
        return false; // Prevent form submission
    } else {
        // Hide error alert if conditions are met
        document.getElementById("errorAlert").style.display = 'none';
    }

    // Simulate form submission (for demo purposes)
    setTimeout(function() {
        hideLoadingSpinner(); // Hide spinner after form submission
        document.getElementById('results').innerHTML = '<p>Form submitted successfully!</p>';
        document.getElementById('results').style.display = 'block'; // Show results
    }, 3000); // Simulate a 3-second delay before hiding spinner and showing success message

    // You would send the form data to your server here using AJAX
    // For example, you can use xhr.send() to send data to the server.

    return true; // Allow form submission (this line can be omitted if you don't actually want the form to submit)
}

