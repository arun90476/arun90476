    Send("{Alt down}{Tab}")  ; Hold Alt and press Tab (first time)
    Sleep(100)               ; Short delay to let Alt+Tab register
    Send("{Tab}")            ; Press Tab again while holding Alt
    Send("{Alt up}")         ; Release Alt key after both Tab presses
