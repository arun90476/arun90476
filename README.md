private static void processFile(String inputFilePath) {
        // Keywords to search for
        String[] keywords = {"Funded", "Not Funded", "Processed"};
        List<String> lines;

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

            // Step 4: Join the result lines into a single string
            String updatedText = String.join("\n", resultLines);

            // Step 5: Write the updated content back to the file
            Files.write(Paths.get(inputFilePath), updatedText.getBytes());

            System.out.println("Unwanted lines removed successfully.");

        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("Error processing the file.");
        }
    }
