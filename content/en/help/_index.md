---
title: Help
---
## Allowing script execution
(On TMC laptops) You may have to allow Visual Studio Code to execute scripts. With your project folder open in VSC, go to *Terminal > New Terminal* (or just select it if it is already open) and enter the command:
```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```
and press Enter.
