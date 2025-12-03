<!DOCTYPE html>
<html>
<head>
    <title>Dynamic Amount Inputs</title>
</head>
<body>
    <form action="process" method="post">
        <label>PO Count: </label>
        <input type="number" id="poCount"  min="1" onchange="generateInputs()">

        <div id="inputsContainer" style="margin-top:10px;"></div>

        <br>
        <input type="submit" value="Submit">
    </form>

    <script>
        function generateInputs() {
            const container = document.getElementById("inputsContainer");
            container.innerHTML = ""; // clear previous inputs

            const count = parseInt(document.getElementById("poCount").value);

            for (let i = 1; i <= count; i++) {
                const input = document.createElement("input");
                input.type = "number";
                input.step = "0.01"; // allow decimals
                input.name = "amount"; // same name for all inputs
                input.placeholder = "Enter amount " + i;
                input.required = true;
                container.appendChild(input);

                // Add line break
                container.appendChild(document.createElement("br"));
            }
        }

        // Generate default inputs on page load
        window.onload = generateInputs;
    </script>
</body>
</html>
