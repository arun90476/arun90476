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
