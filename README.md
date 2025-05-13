import java.io.*;
import java.util.regex.*;

public class DateFormatChecker {

    public static void main(String[] args) {
        String filePath = "your_file_path.txt";  // Replace with your file path
        String regex = "\\b(0[1-9]|[12][0-9]|3[01])/(0[1-9]|1[0-2])/(\\d{4})\\b";  // Regex for dd/mm/yyyy format
        
        try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
            String line;
            Pattern pattern = Pattern.compile(regex);
            int lineNumber = 0;
            
            while ((line = br.readLine()) != null) {
                lineNumber++;
                Matcher matcher = pattern.matcher(line);
                while (matcher.find()) {
                    System.out.println("Line " + lineNumber + ": " + line);
                    System.out.println("Found date: " + matcher.group());
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
