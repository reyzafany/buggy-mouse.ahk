# buggy-mouse.ahk
Fork of same name by bhackel that forked it out from JSLover. Fix a buggy mouse. Stop it from double-clicking when you try to single-click.

Original file was hosted on http://jslover.secsrv.net/AutoHotkey/Scripts/Buggy-Mouse but has since been removed

### Changelog

#### Version 1.1.0

- **Feature: Dynamic Primary Button Detection**
  - Added functionality to detect the current primary mouse button (left or right) using the `GetSystemMetrics` API. This ensures that the script dynamically adapts to the user's primary mouse button setting, whether it's set to **left-click** or **right-click** as the primary button in Windows.
  - Implemented the `GetPrimaryMouseButton()` function to manage this detection.

- **Improvement: Dynamic Button Handling**
  - Refactored the script to use the detected primary mouse button for handling mouse down and up events. The script now works seamlessly regardless of which button (left or right) is configured as the primary mouse button, ensuring the double-click prevention works as expected in all configurations.
