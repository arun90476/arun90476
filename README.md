import java.io.*;
import java.nio.file.*;
import java.util.*;

public class RemoveEmptyLines {
    public static void main(String[] args) {
        String inputFilePath = "path/to/your/inputfile.txt";  // Path to your input file
        String outputFilePath = "path/to/your/outputfile.txt";  // Path to output file

        try {
            // Read all lines from the input file
            List<String> lines = Files.readAllLines(Paths.get(inputFilePath));

            // Create a list to store non-empty lines
            List<String> nonEmptyLines = new ArrayList<>();

            // Iterate through the lines and add only non-empty lines
            for (String line : lines) {
                if (!line.trim().isEmpty()) {  // Ignore empty or whitespace-only lines
                    nonEmptyLines.add(line);
                }
            }

            // Write the non-empty lines to the output file
            Files.write(Paths.get(outputFilePath), nonEmptyLines);

            System.out.println("Empty lines removed and saved to: " + outputFilePath);

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
