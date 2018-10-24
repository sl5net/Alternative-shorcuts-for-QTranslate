# Alternative-shorcuts-for-QTranslate
At the moment I use QTranslate Version  6.7.1.


<code>
;/¯¯¯¯ QTranslateVoiceReader ¯¯ 181024084514 ¯¯ 24.10.2018 08:45:14 ¯¯\
#IfWinActive,
^i::

WinGetActiveTitle, activeTitle
Last_A_This:=A_ThisFunc . A_ThisLabel
ToolTip1sec(A_LineNumber . " " . A_ScriptName . " " . Last_A_This )

send,^+i
winTitle := "QTranslate ahk_class #32770 ahk_exe QTranslate.exe"
tooltip,% "WinWaitActive (" A_LineNumber " " RegExReplace(A_LineFile,".*\\") ")"	
DetectHiddenWindows,Off
WinWaitActive,% winTitle,,3
IfWinNotActive,% winTitle
{
	Msgbox,,% ":( WinNotExistActive " winTitle " `n (" A_LineNumber " " RegExReplace(A_LineFile,".*\\") ")",,3
	return
}
; Wait until it doesn't change:
transEnglish1 := ""
transEnglish2 := ""
transEnglish3 := ""
while(true){
	tooltip,% "while (" A_LineNumber " " RegExReplace(A_LineFile,".*\\") ")"	
	Sleep,400
	ControlGetText, transEnglish3 , RICHEDIT50W2, % winTitle
	if(!transEnglish3) ; This probably never happens
		continue
	if(a_index == 1)
		transEnglish1 := transEnglish3
	isChangedInLastStep := (transEnglish2 <> transEnglish3) 
	if(!isChangedInLastStep && transEnglish3 <> transEnglish1)
		break
	transEnglish2 := transEnglish3
	aindex := (isChangedInLastStep) ? 1 : aindex++
	if(aindex > 20) 
		return
}
; You may also want to have the original German version later
ControlGetText, transGermanSTART  , RICHEDIT50W1, % winTitle

Clipboard := transEnglish3
WinActivate,% activeTitle
tooltip,% "WinWaitActive (" A_LineNumber " " RegExReplace(A_LineFile,".*\\") ")"
WinWaitActive,% activeTitle,,2
Send,^v

Sleep,1000
Clipboard := transGermanSTART
WinClose, % winTitle
tooltip,% "WinWaitClose (" A_LineNumber " " RegExReplace(A_LineFile,".*\\") ")",1,1
WinWaitClose,,,3
tooltip,
return
;\____ QTranslateVoiceReader __ 181024084505 __ 24.10.2018 08:45:05 __/

</code>
