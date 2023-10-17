## Build and compile with Visual Studio 2019
1. 项目根目录下执行 ./build.bat
2. 使用 NSIS 构建install exe文件：a) Compile NSI scripts b) File -> Load script... -> installer/installer.nsi

## 更好的 IPC 架構
https://github.com/EasyIME/forum/issues/11

## 开发(reload ime service)
参考： https://github.com/EasyIME/PIME/issues/50
已经安装的输入法，如果需要修改生效，则结束node或者python进程即可，会自动重启新进程（在任务管理器在可以查看进程的pid发生了变化）。

## Log日志(win 11 中可以搜索 `%AppData%` 快速定位到)
C:\Users\<user>\AppData\Local\PIME\Log 

## pip install packages
`python/python3/virtualenv/Scripts/python.exe -m pip install -r requirements.txt`

# PIME

[![Build status](https://ci.appveyor.com/api/projects/status/cwfb9moce0dss7gs?svg=true)](https://ci.appveyor.com/project/dongyuwei/pime)

以下为PIME原项目文档
=================

Implement input methods easily for Windows via Text Services Framework:
*   LibIME contains a library which aims to be a simple wrapper for Windows Text Service Framework (TSF).
*   PIMETextService contains an backbone implementation of Windows text service for using libIME.
*   The python server part requires python 3.x and pywin32 package.

All parts are licensed under GNU LGPL v2.1 license.

# Development

## Tool Requirements
*   [CMake](http://www.cmake.org/) >= 3.0
*   [Visual Studio 2019](https://visualstudio.microsoft.com/vs)
*   [git](http://windows.github.com/)

## How to Build
*   Get source from github.

        git clone https://github.com/EasyIME/PIME.git
        cd PIME
        git submodule update --init

*   Use the following CMake commands to generate Visual Studio project.

        cmake -G "Visual Studio 16 2019" -A Win32 <path to PIME source folder>
        cmake -G "Visual Studio 16 2019" -A x64 <path to PIME source folder>

*   Open generated project with Visual Studio and build it.

## TSF References
*   [Text Services Framework](http://msdn.microsoft.com/en-us/library/windows/desktop/ms629032%28v=vs.85%29.aspx)
*   [Guidelines and checklist for IME development (Windows Store apps)](http://msdn.microsoft.com/en-us/library/windows/apps/hh967425.aspx)
*   [Input Method Editors (Windows Store apps)](http://msdn.microsoft.com/en-us/library/windows/apps/hh967426.aspx)
*   [Third-party input method editors](http://msdn.microsoft.com/en-us/library/windows/desktop/hh848069%28v=vs.85%29.aspx)
*   [Strategies for App Communication between Windows 8 UI and Windows 8 Desktop](http://software.intel.com/en-us/articles/strategies-for-app-communication-between-windows-8-ui-and-windows-8-desktop)
*   [TSF Aware, Dictation, Windows Speech Recognition, and Text Services Framework. (blog)](http://blogs.msdn.com/b/tsfaware/?Redirected=true)
*   [Win32 and COM for Windows Store apps](http://msdn.microsoft.com/en-us/library/windows/apps/br205757.aspx)
*   [Input Method Editor (IME) sample supporting Windows 8](http://code.msdn.microsoft.com/windowsdesktop/Input-Method-Editor-IME-b1610980)

## Windows ACL (Access Control List) references
*   [The Windows Access Control Model Part 1](http://www.codeproject.com/Articles/10042/The-Windows-Access-Control-Model-Part-1#SID)
*   [The Windows Access Control Model: Part 2](http://www.codeproject.com/Articles/10200/The-Windows-Access-Control-Model-Part-2#SidFun)
*   [Windows 8 App Container Security Notes - Part 1](http://recxltd.blogspot.tw/2012/03/windows-8-app-container-security-notes.html)
*   [How AccessCheck Works](http://msdn.microsoft.com/en-us/library/windows/apps/aa446683.aspx)
*   [GetAppContainerNamedObjectPath function (enable accessing object outside app containers using ACL)](http://msdn.microsoft.com/en-us/library/windows/desktop/hh448493)
*   [Creating a DACL](http://msdn.microsoft.com/en-us/library/windows/apps/ms717798.aspx)

# Install
*   Copy `PIMETextService.dll` to C:\Program Files (X86)\PIME\x86\.
*   Copy `PIMETextService.dll` to C:\Program Files (X86)\PIME\x64\.
*   Copy the folder `python` to `C:\Program Files (X86)\PIME\`
*   Copy the folder `node` to `C:\Program Files (X86)\PIME\`
*   Use `regsvr32` to register `PIMETextService.dll`. 64-bit system need to register both 32-bit and 64-bit `PIMETextService.dll`

        regsvr32 "C:\Program Files (X86)\PIME\x86\PIMETextService.dll" (run as administrator)
        regsvr32 "C:\Program Files (X86)\PIME\x64\PIMETextService.dll" (run as administrator)

*   NOTICE: the `regsvr32` command needs to be run as Administrator. Otherwise you'll get access denied error.
*   In Windows 8, if you put the dlls in places other than C:\Windows or C:\Program Files, they will not be accessible in metro apps.

# Uninstall
*   Use `regsvr32` to unregister `PIMETextService.dll`. 64-bit system need to unregister both 32-bit and 64-bit `PIMETextService.dll`

        regsvr32 /u "C:\Program Files (X86)\PIME\x86\PIMETextService.dll" (run as administrator)
        regsvr32 /u "C:\Program Files (X86)\PIME\x64\PIMETextService.dll" (run as administrator)
*   Remove `C:\Program Files (X86)\PIME`

*   NOTICE: the `regsvr32` command needs to be run as Administrator. Otherwise you'll get access denied error.

# Bug Report
Please report any issue to [here](https://github.com/EasyIME/PIME/issues).
