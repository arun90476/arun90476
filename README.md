private static String processText(String text) {
        // Keywords to search for in the extracted text
        String[] keywords = {"Funded", "Not Funded", "Processed"};

        String[] lines = text.split("\n");  // Split the text into lines
        StringBuilder filteredText = new StringBuilder();
        boolean foundKeyword = false;

        // Iterate through the lines and start adding lines once a keyword is found
        for (String line : lines) {
            if (!foundKeyword) {
                for (String keyword : keywords) {
                    if (line.contains(keyword)) {
                        foundKeyword = true;
                        break;
                    }
                }
            }

            if (foundKeyword) {
                filteredText.append(line).append("\n");  // Add the line if after a keyword match
            }
        }

        return filteredText.toString().trim();  // Return the processed text
    }
