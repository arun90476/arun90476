 // Keywords to search for
        String[] keywords = {"Funded", "Not Funded", "Processed"};
        String targetText = "11380490"; // The text to search for in the remaining content
        List<String> lines;
        int position = -1;  // Position of the first match (line number of targetText)

        try {
            // Step 1: Read all lines from the file
            lines = Files.readAllLines(Paths.get(inputFilePath));

            // Step 2: Flag to indicate if the first occurrence has been found
            boolean foundKeyword = false;
            List<String> resultLines = new ArrayList<>();

            // Step 3: Iterate through the lines of text
            for (int i = 0; i < lines.size(); i++) {
                String line = lines.get(i);
                if (!foundKeyword) {
                    // Check if the line contains any of the keywords
                    for (String keyword : keywords) {
                        if (line.contains(keyword)) {
                            // Once the keyword is found, add the current line and all subsequent lines
                            foundKeyword = true;
                            resultLines.add(line);  // Add the line with the keyword
                            break; // Stop checking further keywords after finding one
                        }
                    }
                } else {
                    // Add all subsequent lines to resultLines
                    resultLines.add(line);
                }
            }

            System.out.println(resultLines.size());
            // Step 4: Now search for the line containing targetText ("11380192")
            for (int i = 0; i<resultLines.size(); i++) {
                if (resultLines.get(i).contains(targetText)) {
                    position = i+1; 
                    break;
                }
            }

            // Step 5: Join the result lines into a single string
            String updatedText = String.join("\n", resultLines);

            // Step 6: Write the updated content back to the file
            Files.write(Paths.get(inputFilePath), updatedText.getBytes());

            // Step 7: Return the position (line number where "11380192" is found)
            return position;

        } catch (IOException e) {
            e.printStackTrace();
            return -1;  // Return -1 in case of error
        }
    }

    public static void main(String[] args) {
        String filePath = "C:\\Users\\Arun prasad\\OneDrive\\Pictures\\demo.txt";  // Replace with your actual file path

        // Call the processFile function to remove lines before the first keyword match and find "11380192"
        int position = processFile(filePath);

        if (position != -1) {
            System.out.println("The position of the line containing '11380192' in the modified text is: " + position);
        } else {
            System.out.println("Error processing the file or target text not found.");
        }
    }
