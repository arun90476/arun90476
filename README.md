If $i == 1 Then
		MouseMove(252, 140) ; Coordinates for the '5' button (change as necessary)
        MouseClick("left")
        Sleep(2000)
    Else
        Send("{DOWN}")
    EndIf

    ; Wait a moment before the next key press
    Sleep(2000) ; Adjust sleep time as needed for the action to register

    ; After each iteration, check if the specific text is found (i.e., $lineNumber)
    If $i == $lineNumber Then


       MouseMove(57, 770) ; Coordinates for another button
       MouseClick("left")
       Sleep(5000)

	   Send("{ENTER}")
