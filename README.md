<!DOCTYPE html>
<html>
<head>
    <title>DSR Report</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #007bff;
            color: white;
        }
        .container {
            width: 90%;
            margin: auto;
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #007bff;
            color: white;
            padding: 10px;
        }
        .status {
            background-color: green;
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: bold;
        }
        .edit-btn, .save-btn {
            background-color: #28a745;
            color: white;
            padding: 5px 10px;
            border: none;
            cursor: pointer;
            margin-left: 5px;
        }
        .save-btn {
            display: none;
        }
        .dsr-management {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            background-color: #f9f9f9;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h2>DSR Unified Daily Test Status</h2>
            <div>
                <label for="dsrSelect">Select DSR:</label>
                <select id="dsrSelect" onchange="switchDSR()"></select>
                <span class="status" id="dsrStatus">Green</span>
                <button class="edit-btn" onclick="enableEditing()">Edit Report</button>
                <button class="save-btn" id="saveButton" onclick="saveReport()">Save Report</button>
            </div>
        </div>
        
        <div class="dsr-management">
            <h3>Manage DSRs</h3>
            <input type="text" id="newDsrInput" placeholder="Enter new DSR name">
            <button onclick="addNewDSR()">Add DSR</button>
            <input type="text" id="renameDsrInput" placeholder="Rename selected DSR">
            <button onclick="renameDSR()">Rename DSR</button>
            <button onclick="removeDSR()">Remove DSR</button>
        </div>
        
        <h3>Report Details</h3>
        <table>
            <tr>
                <th>Report Date</th>
                <td data-id="reportDate" contenteditable="false">10-Feb-25</td>
                <th>Project Number</th>
                <td data-id="projectNumber" contenteditable="false"></td>
            </tr>
            <tr>
                <th>Project Manager</th>
                <td data-id="projectManager" contenteditable="false">Bailur, Mandar</td>
                <th>Project Name</th>
                <td data-id="projectName" contenteditable="false">DDE PPC Threshold</td>
            </tr>
            <tr>
                <th>Scrum Master</th>
                <td data-id="scrumMaster" contenteditable="false">L, Nizammudin</td>
                <th>Go-Live Date</th>
                <td data-id="goLiveDate" contenteditable="false">22-Feb-25</td>
            </tr>
        </table>
        <h3>Test Schedule</h3>
        <table>
            <tr>
                <th>Phase</th>
                <th>Planned Start Date</th>
                <th>Planned End Date</th>
                <th>Actual Start Date</th>
                <th>Actual End Date</th>
            </tr>
            <tr>
                <td>Plan</td>
                <td data-id="planStart" contenteditable="false">26-Nov-24</td>
                <td data-id="planEnd" contenteditable="false">28-Nov-24</td>
                <td data-id="actualStart" contenteditable="false">26-Nov-24</td>
                <td data-id="actualEnd" contenteditable="false">28-Nov-24</td>
            </tr>
        </table>
        
        <h3>Defect Summary</h3>
        <table>
            <tr>
                <th>Severity</th>
                <th>Closed</th>
                <th>Open</th>
                <th>Pending Test</th>
                <th>Grand Total</th>
            </tr>
            <tr>
                <td>Critical</td>
                <td data-id="closedDefects" contenteditable="false">40</td>
                <td data-id="openDefects" contenteditable="false">3</td>
                <td data-id="pendingDefects" contenteditable="false">0</td>
                <td data-id="totalDefects" contenteditable="false">23</td>
            </tr>
        </table>

        <h3>RAID Log</h3>
        <table>
            <tr>
                <th>Sr. No.</th>
                <th>Type</th>
                <th>Description</th>
                <th>Date Logged</th>
                <th>Target Closure Date</th>
                <th>Owner</th>
                <th>Status</th>
                <th>RAG</th>
                <th>Back to Green Plan</th>
            </tr>
            <tr>
                <td>1</td>
                <td>D</td>
                <td data-id="raidDesc" contenteditable="false">Cosmetic issue in Repair screen for PO level repair</td>
                <td data-id="raidDateLogged" contenteditable="false">30-Jan-25</td>
                <td data-id="raidClosureDate" contenteditable="false">7-Feb-25</td>
                <td data-id="raidOwner" contenteditable="false">CQE</td>
                <td data-id="raidStatus" contenteditable="false">Closed</td>
                <td data-id="raidRAG" contenteditable="false">Green</td>
                <td data-id="raidPlan" contenteditable="false">Issue fixed and retested</td>
            </tr>
        </table>
        
    </div>

<script>
    function enableEditing() {
        document.querySelectorAll("td[contenteditable='false']").forEach(cell => {
            cell.setAttribute("contenteditable", "true");
            cell.style.backgroundColor = "#f3f3f3";
        });
        document.getElementById("saveButton").style.display = "inline-block";
    }

    function saveReport() {
        let reportData = {};
        document.querySelectorAll("td[contenteditable='true']").forEach(cell => {
            let key = cell.getAttribute("data-id");
            if (key) {
                reportData[key] = cell.innerText.trim();
            }
            cell.setAttribute("contenteditable", "false");
            cell.style.backgroundColor = "";
        });

        // Send report data to backend via AJAX
        fetch("/webProject/dsrReport", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(reportData)
        })
        .then(response => response.json())
        .then(data => {
            if (data.success) {
                alert("Report saved successfully!");
                document.getElementById("saveButton").style.display = "none";
            } else {
                alert("Error saving report: " + data.error);
            }
        })
        .catch(error => console.error("Error:", error));
    }

    function loadDSRs() {
        let dsrSelect = document.getElementById("dsrSelect");
        dsrSelect.innerHTML = "";
        let dsrs = JSON.parse(localStorage.getItem("dsrList")) || [];

        if (dsrs.length === 0) {
            dsrs.push("Default DSR"); // Ensure at least one DSR exists
            localStorage.setItem("dsrList", JSON.stringify(dsrs));
        }

        dsrs.forEach(dsr => {
            let option = document.createElement("option");
            option.value = dsr;
            option.textContent = dsr;
            dsrSelect.appendChild(option);
        });

        let lastSelected = localStorage.getItem("selectedDSR") || dsrs[0];
        dsrSelect.value = lastSelected;
        localStorage.setItem("selectedDSR", lastSelected);
        loadReport();
    }

    function addNewDSR() {
        let dsrName = document.getElementById("newDsrInput").value.trim();
        if (!dsrName) {
            alert("Enter a valid DSR name.");
            return;
        }
        
        let dsrs = JSON.parse(localStorage.getItem("dsrList")) || [];
        
        if (dsrs.includes(dsrName)) {
            alert("DSR already exists!");
            return;
        }

        dsrs.push(dsrName);
        localStorage.setItem("dsrList", JSON.stringify(dsrs));

        loadDSRs(); // Refresh dropdown list
        document.getElementById("newDsrInput").value = ""; // Clear input field
    }

    function renameDSR() {
        let dsrs = JSON.parse(localStorage.getItem("dsrList")) || [];
        let selectedDSR = document.getElementById("dsrSelect").value;
        let newName = document.getElementById("renameDsrInput").value.trim();
        if (!newName || dsrs.includes(newName)) {
            alert("Enter a valid new name.");
            return;
        }
        
        dsrs[dsrs.indexOf(selectedDSR)] = newName;
        localStorage.setItem("dsrList", JSON.stringify(dsrs));
        localStorage.setItem(newName, localStorage.getItem(selectedDSR));
        localStorage.removeItem(selectedDSR);
        loadDSRs();
    }

    function removeDSR() {
        let dsrs = JSON.parse(localStorage.getItem("dsrList")) || [];
        let selectedDSR = document.getElementById("dsrSelect").value;
        dsrs = dsrs.filter(dsr => dsr !== selectedDSR);
        localStorage.setItem("dsrList", JSON.stringify(dsrs));
        localStorage.removeItem(selectedDSR);
        loadDSRs();
    }

    function switchDSR() {
        localStorage.setItem("selectedDSR", document.getElementById("dsrSelect").value);
        loadReport();
    }

    function loadReport() {
        // Fetch report from backend
        fetch("/webProject/dsrReport")
        .then(response => response.json())
        .then(data => {
            document.querySelectorAll("td[data-id]").forEach(cell => {
                cell.innerText = data[cell.getAttribute("data-id")] || "";
            });
        })
        .catch(error => console.error("Error:", error));
    }

    window.onload = loadDSRs;
</script>
</body>
</html>



package test;

import java.io.*;
import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.*;
import org.json.JSONObject;

@WebServlet("/dsrReport")
public class LoadDSRServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    // Simulating stored report (since no database is used yet)
    private static JSONObject storedReport = null;

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");
        PrintWriter out = response.getWriter();

        if (storedReport != null) {
            out.print(storedReport.toString()); // Send saved report data
        } else {
            out.print("{}"); // Return empty JSON if no report exists
        }
        out.flush();
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("application/json");
        response.setCharacterEncoding("UTF-8");
        PrintWriter out = response.getWriter();

        // Read JSON request data
        StringBuilder jsonBuffer = new StringBuilder();
        String line;
        BufferedReader reader = request.getReader();
        while ((line = reader.readLine()) != null) {
            jsonBuffer.append(line);
        }

        try {
            JSONObject receivedData = new JSONObject(jsonBuffer.toString());
            storedReport = receivedData; // Save report data
            out.print("{\"success\": \"Report saved successfully\"}");
        } catch (Exception e) {
            out.print("{\"error\": \"Invalid JSON format\"}");
        }
        out.flush();
    }
}

