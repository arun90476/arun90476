 // Define the area to capture (100x30 pixels box around the mouse)
            int width = 100;
            int height = 30;
            
            // Create a Robot instance to capture the screenshot
            Robot robot = new Robot();
            Rectangle captureArea = new Rectangle(mouseX, mouseY, width, height);
            BufferedImage screenshot = robot.createScreenCapture(captureArea);

            // Save the screenshot to a file (optional)
            File screenshotFile = new File("screenshot.png");
            ImageIO.write(screenshot, "png", screenshotFile);
            
            // Use Tesseract OCR to extract text from the screenshot
            Tesseract tesseract = new Tesseract();
            tesseract.setLanguage("eng"); // Set language (English here)

            String extractedText = tesseract.doOCR(screenshot);

            // Output the extracted text
            System.out.println("Extracted Text: " + extractedText);

            // Check if the extracted text contains the specific phrase
            String targetText = "specific text";  // Replace with your target text
            if (extractedText.contains(targetText)) {
                System.out.println("Specific text found! Performing action...");
                // Perform your desired action here (e.g., calling an AutoHotkey script, etc.)
            }

            // Delete the screenshot file after processing
            if (screenshotFile.exists()) {
                if (screenshotFile.delete()) {
                    System.out.println("Screenshot file deleted successfully.");
                } else {
                    System.out.println("Failed to delete the screenshot file.");
                }
            }
