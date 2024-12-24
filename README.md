 Thread.sleep(5000);

        Robot robot = new Robot();
        robot.setAutoDelay(3000);

        // Activate the desired window (simplified; replace with specific logic if needed)
        activateWindow();

        // Simulate mouse clicks at specific coordinates
        moveAndClick(robot, 30, 30);
        moveAndClick(robot, 74, 134);
        moveAndClick(robot, 348, 134);
        moveAndClick(robot, 562, 81);

        // Define file paths
        String tesseractPath = "C:\\Program Files\\Tesseract-OCR\\tesseract.exe";
        String screenshotPath = "C:\\Users\\Arun prasad\\OneDrive\\Pictures\\screenshot.png";
        String outputTextFile = "C:\\Users\\Arun prasad\\OneDrive\\Pictures\\demo.txt";

        // Take a screenshot
        captureScreenshot(screenshotPath);

        // Run Tesseract OCR
        String extractedText = runTesseract(tesseractPath, screenshotPath, outputTextFile);

        // Process extracted text (remove text before and including "Level")
        String processedText = processText(extractedText);

        // Save the processed text back to the file
        Files.write(Paths.get(outputTextFile), processedText.getBytes(StandardCharsets.UTF_8));

        // Search for the target text
        String searchText = "11380228";
        int lineNumber = searchForLine(processedText, searchText);
        System.out.println("Line number"+lineNumber);
        
        // Perform GUI actions based on search results
        if (lineNumber > 0) {
            performKeyPresses(robot, lineNumber);
        } else {
            System.out.println("Text not found.");
        }

        // Call AutoIt script to simulate key presses
      
    }

    // Helper Methods

    /**
     * Activate the target window.
     */
    private static void activateWindow() {
        // Use JNA or external libraries to activate the specific window
        // This placeholder assumes the window is already active
        System.out.println("Ensure the target window is active.");
    }
    
    
    public static void setClipboardContent(String text) {
        StringSelection stringSelection = new StringSelection(text);
        Clipboard clipboard = Toolkit.getDefaultToolkit().getSystemClipboard();
        clipboard.setContents(stringSelection, null);
        System.out.println("Text copied to clipboard: " + text);
    }

    /**
     * Simulate pressing Ctrl + V using the Robot class.
     * @throws InterruptedException 
     */
    public static void simulateCtrlV() throws AWTException, InterruptedException {
        Robot robot = new Robot();

        // Ensure the window where you want to paste has focus. You can add logic here to switch windows if needed.

        // Simulate pressing Ctrl key
        robot.keyPress(KeyEvent.VK_CONTROL);

        // Simulate pressing V key
        robot.keyPress(KeyEvent.VK_V);

        Thread.sleep(2000);
        // Simulate releasing V key
        robot.keyRelease(KeyEvent.VK_V);

        // Simulate releasing Ctrl key
        robot.keyRelease(KeyEvent.VK_CONTROL);

        System.out.println("Ctrl + V simulated to paste clipboard content.");
    }
    /**
     * Simulate mouse click at specific coordinates.
     */
    private static void moveAndClick(Robot robot, int x, int y) {
        robot.mouseMove(x, y);
        robot.mousePress(InputEvent.BUTTON1_DOWN_MASK);
        robot.mouseRelease(InputEvent.BUTTON1_DOWN_MASK);
    }

    /**
     * Run Tesseract OCR to extract text from the screenshot.
     */
    private static String runTesseract(String tesseractPath, String imagePath, String outputTextFile) throws IOException, InterruptedException {
        ProcessBuilder pb = new ProcessBuilder(tesseractPath, imagePath, outputTextFile.replace(".txt", ""));
        pb.redirectErrorStream(true);
        Process process = pb.start();
        process.waitFor();

        // Verify if the output file exists
        if (!Files.exists(Paths.get(outputTextFile))) {
            throw new IOException("Tesseract output file not found.");
        }

        // Read the output file
        return new String(Files.readAllBytes(Paths.get(outputTextFile)), StandardCharsets.UTF_8);
    }

    /**
     * Process the extracted text to remove everything before and including "Level".
     */
    private static String processText(String text) {
        int index = text.indexOf("Level");
        // Remove everything before and including "Level"
        return (index >= 0) ? text.substring(index + "Level".length()).trim() : text;
    }

    /**
     * Search for the specific text in the processed output and return the line number.
     */
    private static int searchForLine(String text, String searchText) {
        String[] lines = text.split("\n");
        for (int i = 1; i <= lines.length; i++) {
            if (lines[i].contains(searchText)) {
                System.out.println("Text found at line " + i+1);
                System.out.println("Text" + lines[1]);
                return i; // Return line number
            }
        }
        return -1; // Text not found
    }

    /**
     * Simulate key presses based on the number of iterations.
     * @throws AWTException 
     */
    private static void performKeyPresses(Robot robot, int iterations) throws InterruptedException, AWTException {
        for (int i = 1; i <= iterations; i++) {
            if (i == 1) {
            	moveAndClick(robot,108, 134);
                Thread.sleep(2000); // Wait for the action to complete
            }
            else if(iterations==i)
            {
          	     callAutoItScript("DOWN");

            	  callAutoItScript("ENTER");
                  Thread.sleep(5000); // Wait for application to process the action

                  callAutoItScript("DELETE");
                  Thread.sleep(5000);
                  
                  setClipboardContent("2620000011");
                  simulateCtrlV();
                  
                  Thread.sleep(3000);

                  callAutoItScript("TAB");
                  callAutoItScript("TAB");
                  callAutoItScript("TAB");
                  callAutoItScript("TAB");
                  callAutoItScript("TAB");
                  
                  Thread.sleep(3000);
            	  callAutoItScript("ENTER");


            }
        
            
            else
            {
            	  callAutoItScript("DOWN");
                  Thread.sleep(3000); // Wait for application to process the action

            }
        }
    }

    /**
     * Capture a screenshot of the entire desktop.
     */
    private static void captureScreenshot(String screenshotPath) throws Exception {
        Robot robot = new Robot();
        Rectangle screenRect = new Rectangle(Toolkit.getDefaultToolkit().getScreenSize());
        BufferedImage screenCapture = robot.createScreenCapture(screenRect);
        ImageIO.write(screenCapture, "png", new File(screenshotPath));
        System.out.println("Screenshot saved to: " + screenshotPath);
    }

    /**
     * Call AutoIt script to simulate pressing Down, Tab, and Enter keys.
     */
    private static void callAutoItScript(String key) {
        try {
            // Path to the AutoIt interpreter (AutoIt3.exe)
            String autoItInterpreterPath = "C:\\Program Files (x86)\\AutoIt3\\AutoIt3.exe";
            String autoItScriptPath="";
            
            // Path to the AutoIt script (down.au3)
            if(key.equals("ENTER"))
            {
            autoItScriptPath = "C:\\Users\\Arun prasad\\OneDrive\\Documents\\AutoIt demo\\enter.au3";
            }
            else if(key.equals("TAB"))
            {
            autoItScriptPath = "C:\\Users\\Arun prasad\\OneDrive\\Documents\\AutoIt demo\\tab.au3";
            }
            else if(key.equals("DOWN"))
            {
             autoItScriptPath = "C:\\Users\\Arun prasad\\OneDrive\\Documents\\AutoIt demo\\down.au3";
            }
            else if(key.equals("DELETE"))
            {
             autoItScriptPath = "C:\\Users\\Arun prasad\\OneDrive\\Documents\\AutoIt demo\\delete.au3";
            }
            // Use ProcessBuilder to run the AutoIt script
            ProcessBuilder processBuilder = new ProcessBuilder(autoItInterpreterPath, autoItScriptPath);
            Process process = processBuilder.start();
            process.waitFor(); // Wait for the script to finish executing
            System.out.println("AutoIt script executed successfully.");
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
