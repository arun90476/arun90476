; Set the paths
tesseractPath := "C:\Program Files\Tesseract-OCR\tesseract.exe"  ; Path to Tesseract executable
imagePath := "C:\path\to\your\image.png"  ; Path to the image file

; Run Tesseract OCR
Run, % tesseractPath " " imagePath, , Hide  ; This will save the output as "image.txt" in the same folder

; Optional: Show a message when done
MsgBox, Tesseract has finished processing the image.
