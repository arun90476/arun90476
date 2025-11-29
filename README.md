<!DOCTYPE html>
<html>
<head>
    <title>Dropdown Enable Example</title>
</head>
<body>

    <!-- First dropdown -->
    <label>Select Option:</label>
    <select id="first" onchange="toggleSecond()">
        <option value="">-- Select --</option>
        <option value="yes">Yes</option>
        <option value="no">No</option>
    </select>

    <br><br>

    <!-- Second dropdown (disabled initially) -->
    <label>Second Dropdown:</label>
    <select id="second" disabled>
        <option value="">-- Choose --</option>
        <option value="opt1">Option 1</option>
        <option value="opt2">Option 2</option>
    </select>

<script>
function toggleSecond() {
    let first = document.getElementById("first").value;
    let second = document.getElementById("second");

    if (first === "yes") {
        second.disabled = false;
    } else {
        second.disabled = true;
        second.value = ""; // reset value
    }
}
</script>

</body>
</html>
