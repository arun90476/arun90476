import java.io.*;
import java.util.Scanner;

public class RunAHKScriptInline {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Ask for the number to be passed to the AHK script
        System.out.print("Enter the number to copy and paste: ");
        String inputNumber = scanner.nextLine();

        try {
            // Define the path to your AutoHotkey executable (adjust this path)
            String ahkPath = "C:/Program Files/AutoHotkey/AutoHotkey.exe";  // Adjust the path if necessary

            // Build the inline AutoHotkey script as a single string
            String ahkScript = 
                "Clipboard := \"" + inputNumber + "\"\n" +  // Set the clipboard to the input number
                "Send, ^v\n";  // Simulate pressing Ctrl + V (paste)

            // Write the AHK script to a temporary file
            File tempScriptFile = File.createTempFile("temp_ahk_script_", ".ahk");
            BufferedWriter writer = new BufferedWriter(new FileWriter(tempScriptFile));
            writer.write(ahkScript);
            writer.close();

            // Build the command to execute the temporary AHK script
            String command = "\"" + ahkPath + "\" \"" + tempScriptFile.getAbsolutePath() + "\"";

            // Execute the command
            Process process = Runtime.getRuntime().exec(command);

            // Wait for the process to finish
            process.waitFor();
            System.out.println("AHK Script executed successfully.");

            // Delete the temporary AHK script file after execution
            tempScriptFile.delete();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        } finally {
            scanner.close();  // Close the scanner
        }
    }
}
