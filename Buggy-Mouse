
/*
**    Buggy-Mouse.ahk - Fix a buggy mouse. Stop it from double-clicking when you try to single-click.
**    Authors: JSLover - Forked by bhackel, updated using chatgpt-4o
**    AutoHotkey 1.1+
**
*/

#SingleInstance force

; **************************** Settings ****************************
DoubleClickMin_ms := 90  ; Minimum double-click time to block rapid double-clicks.
; **************************** /Settings ****************************

; *** Tray Menu Setup ***
Text_ClicksBlocked := "Clicks Blocked"
Menu, Tray, Add, %Text_ClicksBlocked%, ShowClicksBlocked
Menu, Tray, Default, %Text_ClicksBlocked%
Menu, Tray, NoStandard

; Detect primary mouse button setting
PrimaryButton := GetPrimaryMouseButton()

; Handle primary mouse button down
*%PrimaryButton%:: *MButton:: *RButton::
    ProcessMouseDown(A_ThisHotkey)
Return

; Handle primary mouse button up
*%PrimaryButton% up:: *MButton up:: *RButton up::
    ProcessMouseUp(A_ThisHotkey)
Return

; Update Tray Menu with click block count
UpdateTray:
    BlockedCount_Total := BlockedCount_Down + BlockedCount_Up
    MenuText := Text_ClicksBlocked ": " BlockedCount_Total
    Menu, Tray, Tip, %MenuText% - %A_ScriptName%
Return

; Show clicks blocked info
ShowClicksBlocked:
    MsgBox, 64,, %Text_ClicksBlocked% - Down: %BlockedCount_Down% Up: %BlockedCount_Up%
Return

; Mouse down handler
ProcessMouseDown(hotkey) {
    Critical
    VarSafeHotkey := MakeVarSafe(hotkey)
    TimeSinceLastDown := A_TickCount - LastMouseDown_ts

    If (hotkey = LastMouseDown && TimeSinceLastDown <= DoubleClickMin_ms) {
        BlockedCount_Down++
        Gosub, UpdateTray
    } Else {
        Send, {Blind}{%Hotkey_GetKeyName(hotkey)% DownTemp}
    }
    LastMouseDown := hotkey
    LastMouseDown_ts := A_TickCount
}

; Mouse up handler
ProcessMouseUp(hotkey) {
    Critical
    VarSafeHotkey := MakeVarSafe(hotkey)

    If (blockeddown) {
        BlockedCount_Up++
        Gosub, UpdateTray
    } Else {
        Send, {Blind}{%Hotkey_GetKeyName(hotkey)% up}
    }
    blockeddown := 0
    LastMouseUp_ts := A_TickCount
}

; Utility: Make hotkey safe for variable names
MakeVarSafe(hotkey) {
    return RegExReplace(hotkey, "i)[^a-z0-9_]", "_")
}

; Utility: Get key name without modifiers
Hotkey_GetKeyName(hotkey) {
    hotkey := RegExReplace(hotkey, "i)^[^a-z0-9_]+")  ; Remove modifiers
    return StrSplit(hotkey, " ")[1]  ; Get key name
}

; Utility: Detect current primary mouse button (left or right)
GetPrimaryMouseButton() {
    ; 0 = Left is primary, 1 = Right is primary
    if (DllCall("GetSystemMetrics", "int", 23) = 0) {
        return "LButton"
    } else {
        return "RButton"
    }
}

^+#!F9::Suspend
^+#!F12::ExitApp
