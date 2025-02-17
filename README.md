import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import java.io.*;
import java.util.*;

public class TestCaseGenerator {
    public static void main(String[] args) {
        String inputFile = "frd.txt";  // Replace with your FRD file
        List<String> requirements = readFRD(inputFile);
        List<TestCase> testCases = generateTestCases(requirements);
        writeToExcel(testCases, "TestCases.xlsx");
    }

    // Read Functional Requirements Document (FRD)
    private static List<String> readFRD(String filePath) {
        List<String> requirements = new ArrayList<>();
        try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = br.readLine()) != null) {
                if (line.toLowerCase().contains("requirement:")) {  // Simple keyword-based extraction
                    requirements.add(line.replace("Requirement:", "").trim());
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        return requirements;
    }

    // Generate test cases from requirements
    private static List<TestCase> generateTestCases(List<String> requirements) {
        List<TestCase> testCases = new ArrayList<>();
        int id = 1;
        for (String req : requirements) {
            testCases.add(new TestCase("TC_" + id, req, "Verify " + req, "Expected outcome", "PASS/FAIL"));
            id++;
        }
        return testCases;
    }

    // Write test cases to an Excel file
    private static void writeToExcel(List<TestCase> testCases, String fileName) {
        try (Workbook workbook = new XSSFWorkbook(); FileOutputStream fileOut = new FileOutputStream(fileName)) {
            Sheet sheet = workbook.createSheet("Test Cases");
            Row headerRow = sheet.createRow(0);
            String[] headers = {"Test Case ID", "Requirement", "Test Steps", "Expected Result", "Status"};
            for (int i = 0; i < headers.length; i++) {
                headerRow.createCell(i).setCellValue(headers[i]);
            }

            int rowNum = 1;
            for (TestCase tc : testCases) {
                Row row = sheet.createRow(rowNum++);
                row.createCell(0).setCellValue(tc.id);
                row.createCell(1).setCellValue(tc.requirement);
                row.createCell(2).setCellValue(tc.steps);
                row.createCell(3).setCellValue(tc.expectedResult);
                row.createCell(4).setCellValue(tc.status);
            }

            workbook.write(fileOut);
            System.out.println("Test cases saved to " + fileName);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// Helper class for Test Cases
class TestCase {
    String id, requirement, steps, expectedResult, status;
    
    public TestCase(String id, String requirement, String steps, String expectedResult, String status) {
        this.id = id;
        this.requirement = requirement;
        this.steps = steps;
        this.expectedResult = expectedResult;
        this.status = status;
    }
}
