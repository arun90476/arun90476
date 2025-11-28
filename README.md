

package com.example;


import java.io.*;
import java.nio.file.*;
import java.util.*;

public class FlatFileUpdater {

    // -------------------------------------------------------------
    // REUSABLE METHOD 1: Update fixed position in a line
    // Arguments:
    //   line   → the line to update
    //   start  → starting position (1-based index)
    //   length → number of characters to replace
    //   newValue → value to insert (will be padded or trimmed)
    // -------------------------------------------------------------
    public static String updateFieldByPosition(String line, int start, int length, String newValue) {
        int beginIndex = start - 1;
        int endIndex = beginIndex + length;

        StringBuilder sb = new StringBuilder(line);

        // Ensure line length
        while (sb.length() < endIndex) {
            sb.append(" ");
        }

        // Adjust new value length
        if (newValue.length() > length) {
            newValue = newValue.substring(0, length);
        } else if (newValue.length() < length) {
            newValue = String.format("%-" + length + "s", newValue);
        }

        return sb.replace(beginIndex, endIndex, newValue).toString();
    }

    // -------------------------------------------------------------
    // REUSABLE METHOD 2: Insert copies of line 2 at specific location
    // Arguments:
    //   lines           → file content as List<String>
    //   numberOfCopies  → how many new rows to insert
    //   insertAfterLine → index position where new lines must be inserted
    // -------------------------------------------------------------
    public static List<String> insertCopiesOfLine2(
            List<String> lines,
            int numberOfCopies,
            int insertAfterLine
    ) {

        if (lines == null || lines.size() < 2) {
            throw new IllegalArgumentException("File must contain at least 2 lines.");
        }

        if (numberOfCopies <= 0) {
            return lines;
        }

        String line2 = lines.get(1);  // Line 2 (index 1)

        for (int i = 0; i < numberOfCopies; i++) {
            lines.add(insertAfterLine, line2);
            insertAfterLine++; // after every insert, index moves
        }

        return lines;
    }

    // -------------------------------------------------------------
    // METHOD: Update only specific line in file
    // Arguments:
    //   lines      → List of file lines
    //   lineNumber → 1-based line number to update
    //   start      → starting position in line
    //   length     → number of characters to replace
    //   newValue   → value to insert
    // -------------------------------------------------------------
    public static void updateLineInList(List<String> lines, int lineNumber, int start, int length, String newValue) {
        if (lineNumber < 1 || lineNumber > lines.size()) {
            throw new IllegalArgumentException("Invalid line number: " + lineNumber);
        }

        String updatedLine = updateFieldByPosition(lines.get(lineNumber - 1), start, length, newValue);
        lines.set(lineNumber - 1, updatedLine);
    }

    // -------------------------------------------------------------
    // MAIN (example usage)
    // -------------------------------------------------------------
    public static void main(String[] args) {

        String inputPath  = "C:\\Users\\Arun prasad\\OneDrive\\Documents\\input.txt";
        String outputPath = "C:\\Users\\Arun prasad\\OneDrive\\Documents\\output.txt";

        try {
            // -------------------------------------------------------------
            // STEP 1: Read all lines from input file
            // -------------------------------------------------------------
            List<String> allLines = Files.readAllLines(Paths.get(inputPath));

            // -------------------------------------------------------------
            // STEP 2: Update specific line (line 1)
            // -------------------------------------------------------------
            updateLineInList(allLines, 1, 3, 3, "SEE"); // lineNumber=1, start=3, length=3, newValue="SEE"

            // -------------------------------------------------------------
            // STEP 3: Insert copies of line 2 after index 2
            // -------------------------------------------------------------
            insertCopiesOfLine2(allLines, 2, 2); // 2 copies after index 2

            // -------------------------------------------------------------
            // STEP 4: Write final updated lines to output file
            // -------------------------------------------------------------
            Files.write(Paths.get(outputPath), allLines);

            System.out.println("File updated successfully!");

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
