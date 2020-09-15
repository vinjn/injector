### What is it

Single Visual Studio project implementing multiple `DLL injection` techniques (actually 7 different techniques) that work both for 32 and 64 bits. Each technique has its own source code file to make it easy way to read and understand.

The table below makes it easy to understand what's actually implemented and how to use it.

Method                 | 32 bits | 64 bits |  DLL to use                     |
-----------------------|---------|---------|---------------------------------|
 CreateRemoteThread()  | :heavy_check_mark: | :heavy_check_mark: | dllmain_32.dll / dllmain_64.dll |
 NtCreateThreadEx()    | :heavy_check_mark: | :heavy_check_mark: | dllmain_32.dll / dllmain_64.dll |
 QueueUserAPC()        | :heavy_check_mark: | :heavy_check_mark: | dllmain_32.dll / dllmain_64.dll |
 SetWindowsHookEx()    | :heavy_check_mark: | :heavy_check_mark: |  dllpoc_32.dll / dllpoc_64.dll  |
 RtlCreateUserThread() | :heavy_check_mark: | :heavy_check_mark: | dllmain_32.dll / dllmain_64.dll |
 SetThreadContext()    | :heavy_check_mark: | :heavy_check_mark: | dllmain_32.dll / dllmain_64.dll |
 Reflective DLL        | :heavy_check_mark: | :heavy_check_mark: |    rdll_32.dll / rdll_64.dll    |

### How to use it

```
C:\Users\rui>injectAllTheThings_64.exe
injectAllTheThings - rui@deniable.org
Usage: injectAllTheThings.exe -t <option> <process name> <full/path/to/dll>
Options:
  1     DLL injection via CreateRemoteThread()
  2     DLL injection via NtCreateThreadEx()
  3     DLL injection via QueueUserAPC()
  4     DLL injection via SetWindowsHookEx()
  5     DLL injection via RtlCreateUserThread()
  6     DLL injection via Code Cave SetThreadContext()
  7     Reflective DLL injection
```

Needless to say, to be on the safe side, always use `injectAllTheThings_32.exe` to inject into 32 bits processes or `injectAllTheThings_64.exe` to inject into 64 bits processes. Although, you can also use `injectAllTheThings_64.exe` to inject into 32 bits processes. And actually, I didn't implement it but I might have to give it a try later, you can go from [WoW64 to 64 bits](http://blog.rewolf.pl/blog/?p=102). Which is basically what Metasploit 'smart_migrate' does. Have a look [here](https://github.com/rapid7/meterpreter/blob/5e24206d510a48db284d5f399a6951cd1b4c754b/source/common/arch/win/i386/base_inject.c).

Compile for 32 and 64 bits, with our without debugging and have fun.

**Note**: All techniques have been tested successfully in Windows 10 1903 x64 with `notepad.exe`. This has been used for Endpoint Security testing by me, and a few other people I know, as a PoC. Don't ask for help if you are injecting somewhere else and your target is crashing. I'm pretty sure you can debug the issue yourself if you want to re-use the code in your own tools.

**For more information visit**: http://deniable.org/windows/inject-all-the-things 

### Credits

[Reflective DLL injection](https://github.com/stephenfewer/ReflectiveDLLInjection) - Stephen Fewer
