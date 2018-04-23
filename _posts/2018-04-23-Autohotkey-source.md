---
layout: post
title:  "[윈도우즈 필수 프로그램] 오토핫키(Autohotkey) "
subtitle:   "사용 하고 있는 오토핫키 소스"
categories: autohotkey
tags: 
---


```autohotkey
#NoEnv  ; Recommended for performance and compatibility with future AutoHotkey releases.
#KeyHistory 0
SetBatchLines, -1 
Process, Priority,, High
;  #Warn  ; Enable warnings to assist with detecting common errors.
; SendMode Input  ; Recommended for new scripts due to its superior speed and reliability.
; SetWorkingDir %A_ScriptDir%  ; Ensures a consistent starting directory.
; /*
; Alt ->!
; Shift ->+
; Control -> ^
; Win ->#
; */


SetWallpaper("C:\Users\aeue1107\Documents\SETTING\1.jpg") ;시작과 동시에 Group Policy 에 있는 바탕화면 제거 후 검정색 화면으로 변경

^!c::   ; Cnt + Alt + c = copy Class name and msgbox, 
WinGetClass, class, A
MsgBox, The active window's class is "%class%".
Clipboard=%class%
return 

; ^4::  ;if errorlevel example 
; note:="Untitled - Notepad"
; Run, notepad.exe
; WinWait,%note%, , 3
; if ErrorLevel
; {
;     MsgBox, WinWait timed out.
;     return
; }
; else
;     WinMinimize  ; Minimize the window found by WinWait.

SAP_path:="C:\Program Files (x86)\SAP\SapSetup\setup\SAL\SapLogon.s8l"
^!r::Reload  ; Assign Ctrl-Alt-R as a hotkey to restart the script.
!right::SendInput {end}
!left::SendInput {home}
+!left::SendInput {ShiftDown}{home}
+!right::SendInput {ShiftDown}{end}
+!Up::SendInput {ShiftDown}{PgUp}
+!Down::SendInput {ShiftDown}{PgDn}
!4::SendInput,{AltDown}{F4}
::_tel;::015236779231
^+f::run, C:\Users\aeue1107\Documents\setting\Everything-1.3.4.686.x64.Multilingual\Everything.exe
!BackSpace::SendInput,{F3}
!Enter::sendinput,{F8}
::wr::WRITE : / 
!f::sendinput, ^f
!c::Sendinput, ^c
!v::Sendinput, ^v
!a::Sendinput, ^a
!z::Sendinput, ^z
!s::Sendinput, ^s
!x::Sendinput, ^x
#3::sendinput, ^{F6}
^5::sendinput,{F5}
!w::sendinput,^w
::spqj::eastkim64@naver.com
::wlapf::aidenkim2905@gmail.com
ScrollLock::SetWallpaper("C:\Users\aeue1107\Documents\SETTING\1.jpg")
::;SAP::ZAESTFT52
; SAP Login Start ----------
^+s::
::gpath::C:/Users/aeue1107/AidenRoto.github.io
run, C:\Program Files (x86)\SAP\SapSetup\setup\SAL\SapLogon.s8l
WinWait,SAP Logon 720
WinActivate SAP Logon 720
sleep,500
click,313, 94 ,2 
WinWait,SAP
WinActivate SAP
sleep,700
click,177, 167,
sleep,100
sendinput, ^a
sendinput, 505{Tab}
sendinput, ZAESTFT52{Tab}
sendinput, %PW%{enter}
sleep,500
sendinput,se38{enter}
MsgBox, ABAP Editor is ready!
return,
^+~::sendinput, ^+{Esc}
; SAP login End-------
return,

#Space:: ; Win + N을 누르면 Naver 사전 드래그 되어있는 텍스트 검색 
Sendinput, ^c 
ClipWait,  
run, http://m.endic.naver.com/search.nhn?query=%Clipboard% &searchOption=example&preQuery=&forceRedirect=
return,

!Space:: ; Alt + N을 누르면 Chrome 에서 검색
InputBox, SearchTerm, Search
if not ErrorLevel
if SearchTerm <> ""
run, http://m.endic.naver.com/search.nhn?query=%SearchTerm% &searchOption=example&preQuery=&forceRedirect=
; Run  https://www.google.co.kr/search?q=%SearchTerm%  ; for google search.
return


::;today::
sendinput, %A_YYYY%-%A_MM%-%A_DD%-  ; ; today 입력하면 현재 날짜 입력
return,


#IfWinActive ahk_class Chrome_WidgetWin_1  ; Chrome new tab ( Alt + t ) << Like MacOS
!t::sendinput,^t  
#If   

;------Start of Hotkeys for SAP ---------;
#IfWinActive ahk_class SAP_FRONTEND_SESSION; Start of IF statement 
!d::sendinput,^+l  
^1::sendinput,{F1}
!s::sendinput,^s
!Down::sendinput,{F2}
!Up::sendinput,{F3}
+!3::sendinput,+{F1}
!3::sendinput,^{F3}
^!d::  ; Active in SAP
Click, right, 110, 292
sleep,300
sendinput {Down}{Down}{Down}{Down}{Down}
sleep,300
sendinput {enter}
sleep,300
sendinput {enter}
sendinput {enter}
return,
#If ; End of IF statement 
;----End of Hotkeys for SAP ---------;


SetWallpaper(BMPpath) ; Function for changing wallpaper 
{
  SPI_SETDESKWALLPAPER := 20
  SPIF_SENDWININICHANGE := 2  
Return DllCall("SystemParametersInfo", UINT, SPI_SETDESKWALLPAPER, UINT, uiParam, STR, BMPpath, UINT, SPIF_SENDWININICHANGE)
}

^!d::  ; Active in SAP
Click, right, 110, 292
sleep,300
sendinput {Down}{Down}{Down}{Down}{Down}
sleep,300
sendinput {enter}
sleep,300
sendinput {enter}
sendinput {enter}
return,


/* Nothing 

; 비활성 클릭 소스
; AidenSelect(x,y)
; {
; WinGetPos, w_x,w_y,w_w,w_h, Windows Title ;;타이틀 넣기 
; xx =:x
; yy =:y
; lParam := xx|yy«16
; PostMessage, 0x201,1,%lParam%, Internet Explorer_Server1,Select 1st/2nd/3rd Category — Webpage Dialog
; PostMessage, 0x202,0,%lParam%, Internet Explorer_Server1,Select 1st/2nd/3rd Category — Webpage Dialog

; pg:="ABAP Editor: Change Report YKDH_COPY22"
; Aiden(x,y) 
; {
; WinGetPos, w_x,w_y,w_w,w_h, %pg%
; xx := x
; yy := y
; ;오차가 있음 // 윈도우 크기로 예상됨.

; lParam := xx|yy«16
; PostMessage, 0x201,1,%lParam%, 
; PostMessage,% 0x202,0,%lParam%, %pg%
; msgbox %x%,%y%
; }

*/
```