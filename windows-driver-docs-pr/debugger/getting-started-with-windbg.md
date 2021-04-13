---
title: WinDbg 入门（用户模式）
description: WinDbg 是包含在 Windows 调试工具中的内核模式和用户模式调试器。 在此，我们将提供实践练习，这些练习帮助你开始使用 WinDbg 作为用户模式调试器。
ms.date: 04/01/2021
ms.localizationpriority: high
ms.openlocfilehash: 4f6fa751e1e6629e7c1f147bcc1bd628a4f7a1c4
ms.sourcegitcommit: 119a8f0435127a41cd215063200f67cd6eb51ed1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218283"
---
# <a name="getting-started-with-windbg-user-mode"></a>WinDbg 入门（用户模式）

WinDbg 是包含在 Windows 调试工具中的内核模式和用户模式调试器。 在此，我们将提供实践练习，这些练习帮助你开始使用 WinDbg 作为用户模式调试器。

有关如何获取 Windows 调试工具的信息，请参见 [Windows 调试工具（WinDbg、KD、CDB、NTSD）](index.md)。

安装调试工具后，找到 64 位 (x64) 和 32 位 (x86) 版本工具的安装目录。 例如：

- C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64
- C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x86

## <a name="launch-notepad-and-attach-windbg"></a>启动记事本并附加 WinDbg

1. 导航到安装目录，然后打开 WinDbg.exe。

2. 在“文件”菜单上，选择“打开可执行文件”   。 在“打开可执行文件”对话框中，导航到包含 notepad.exe 的文件夹（通常是 C:\\Windows\\System32）。 输入 notepad.exe 作为“文件名称”  。 选择“打开”。

    ![启动记事本后 windbg 的屏幕截图](images/windbggetstart01.png)

3. 在 WinDbg 窗口底部的命令行中，输入以下命令：

    [.sympath srv\*](-sympath--set-symbol-path-.md)

    输出类似于以下内容：

    ```dbgcmd
    Symbol search path is: srv*
    Expanded Symbol search path is: cache*;SRV
    ```

    符号搜索路径指示 WinDbg 查找符号 (PDB) 文件的位置。 调试器需要符号文件来获取有关代码模块的信息（函数名、变量名等）。

    输入此命令，它会通知 WinDbg 进行符号文件的初始查找和加载：

    [.reload](-reload--reload-module-.md)

4. 若要查看 Notepad.exe 模块的符号，请输入以下命令：

    [x notepad!*](x--examine-symbols-.md)

    **注意** 如果没有看到任何输出，请再次输入 [.reload](-reload--reload-module-.md)。

    若要查看 Notepad.exe 模块中包含 main 的符号，请使用如下所示[检查符号](x--examine-symbols-.md)命令来列出与掩码匹配的模块：

    `x notepad!wWin*`

    输出类似于以下内容：

    ```dbgcmd
    00007ff6`6e76b0a0 notepad!wWinMain (wWinMain)
    00007ff6`6e783db0 notepad!wWinMainCRTStartup (wWinMainCRTStartup)
    ```

5. 若要在 notepad!wWinMain 处设置断点，输入以下命令：

    [bu notepad!wWinMain](bp--bu--bm--set-breakpoint-.md)

    若要验证是否已设置断点，请输入以下命令：

    [bl](bl--breakpoint-list-.md)

    输出类似于以下内容：

    ```dbgcmd
    0 e Disable Clear  00007ff6`6e76b0a0     0001 (0001)  0:**** notepad!wWinMain
    ```

6. 若要启动记事本运行，请输入以下命令：

    [g](g--go-.md)

    记事本将一直运行，直到进入“WinMain”函数，然后中断到调试器  。

    ```dbgcmd
    Breakpoint 0 hit
    notepad!wWinMain:
    00007ff6`6e76b0a0 488bc4          mov     rax,rsp
    ```

    若要查看在记事本进程中加载的代码模块列表，请输入以下命令：

    [lm](lm--list-loaded-modules-.md)

    输出类似于以下内容：

    ```dbgcmd
    0:000> lm
    start             end                 module name
    00007ff6`6e760000 00007ff6`6e798000   notepad    (pdb symbols)          C:\ProgramData\Dbg\sym\notepad.pdb\BC04D9A431EDE299D4625AD6201C8A4A1\notepad.pdb
    00007ff8`066a0000 00007ff8`067ab000   gdi32full   (deferred)             
    00007ff8`067b0000 00007ff8`068b0000   ucrtbase   (deferred)             
    00007ff8`06a10000 00007ff8`06aad000   msvcp_win   (deferred)             
    00007ff8`06ab0000 00007ff8`06ad2000   win32u     (deferred)             
    00007ff8`06b40000 00007ff8`06e08000   KERNELBASE   (deferred)             
    00007ff8`07220000 00007ff8`072dd000   KERNEL32   (deferred)             
    00007ff8`07420000 00007ff8`07775000   combase    (deferred)             
    00007ff8`07820000 00007ff8`079c0000   USER32     (deferred)             
    00007ff8`079c0000 00007ff8`079f0000   IMM32      (deferred)             
    00007ff8`07c00000 00007ff8`07c2a000   GDI32      (deferred)             
    00007ff8`08480000 00007ff8`085ab000   RPCRT4     (deferred)             
    00007ff8`085b0000 00007ff8`0864e000   msvcrt     (deferred)             
    00007ff8`08c40000 00007ff8`08cee000   shcore     (deferred)             
    00007ff8`08db0000 00007ff8`08fa5000   ntdll      (pdb symbols)          C:\ProgramData\Dbg\sym\ntdll.pdb\53F12BFE149A2F50205C8D5D66290B481\ntdll.pdb
    00007fff`f8580000 00007fff`f881a000   COMCTL32   (deferred)    
    ```

    若要查看堆栈跟踪，请输入以下命令：

    [k](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

    输出类似于以下内容：

    ```dbgcmd
    0:000> k
    00 000000c8`2647f708 00007ff6`6e783d36     notepad!wWinMain
    01 000000c8`2647f710 00007ff8`07237034     notepad!__scrt_common_main_seh+0x106
    02 000000c8`2647f750 00007ff8`08e02651     KERNEL32!BaseThreadInitThunk+0x14
    03 000000c8`2647f780 00000000`00000000     ntdll!RtlUserThreadStart+0x21
    ```

7. 若要再次启动记事本运行，请输入以下命令：

    [g](g--go-.md)

8. 若要中断记事本，请从“文件”菜单中选择“中断” 。

9. 若要在 ZwWriteFile 设置并验证断点，请输入以下命令  ：

    [bu ntdll!ZwWriteFile](bp--bu--bm--set-breakpoint-.md)

    [bl](bl--breakpoint-list-.md)

10. 输入 [g](g--go-.md) 重新启动记事本。 在“记事本”窗口中，输入一些文本并从“文件”菜单中选择“保存”。 当遇到 ZwCreateFile 时，正在运行的代码会中断  。 输入 [k](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 以查看堆栈跟踪。

    ![windbg 中堆栈跟踪的屏幕截图](images/windbggetstart02.png)

    在 WinDbg 窗口的命令行左侧，注意处理器和线程号。 在本例中，当前处理器号为 0，当前线程号为 11。 因此，我们正在查看线程 11 的堆栈跟踪（它正好在处理器 0 上运行）。

11. 若要查看记事本进程中所有线程的列表，请输入以下命令（波形符）：

    [~](---thread-status-.md)

    输出类似于以下内容：

    ```dbgcmd
    0:011> ~
       0  Id: 5500.34d8 Suspend: 1 Teb: 000000c8`262c4000 Unfrozen
       1  Id: 5500.3960 Suspend: 1 Teb: 000000c8`262c6000 Unfrozen
        2  Id: 5500.5d68 Suspend: 1 Teb: 000000c8`262c8000 Unfrozen
        3  Id: 5500.4c90 Suspend: 1 Teb: 000000c8`262ca000 Unfrozen
        4  Id: 5500.4ac4 Suspend: 1 Teb: 000000c8`262cc000 Unfrozen
        5  Id: 5500.293c Suspend: 1 Teb: 000000c8`262ce000 Unfrozen
        6  Id: 5500.53a0 Suspend: 1 Teb: 000000c8`262d0000 Unfrozen
        7  Id: 5500.3ca4 Suspend: 1 Teb: 000000c8`262d4000 Unfrozen
        8  Id: 5500.808 Suspend: 1 Teb: 000000c8`262da000 Unfrozen
       10  Id: 5500.3940 Suspend: 1 Teb: 000000c8`262dc000 Unfrozen
     . 11  Id: 5500.28b0 Suspend: 1 Teb: 000000c8`262de000 Unfrozen
       12  Id: 5500.12bc Suspend: 1 Teb: 000000c8`262e0000 Unfrozen
       13  Id: 5500.4c34 Suspend: 1 Teb: 000000c8`262e2000 Unfrozen
    ```

    在本例中有 14 个线程，索引为 0-13。

12. 若要查看线程 0 的堆栈跟踪，请输入以下命令：

    [~0s](-s--set-current-thread-.md)

    [k](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

    输出类似于以下内容：

    ```dbgcmd
    0:011> ~0s
    0:011> ~0s
    win32u!NtUserGetProp+0x14:
    00007ff8`06ab1204 c3              ret
    0:000> k
     # Child-SP          RetAddr               Call Site
    00 000000c8`2647bd08 00007ff8`07829fe1     win32u!NtUserGetProp+0x14
    01 000000c8`2647bd10 00007fff`f86099be     USER32!GetPropW+0xd1
    02 000000c8`2647bd40 00007ff8`07d12f4d     COMCTL32!DefSubclassProc+0x4e
    03 000000c8`2647bd90 00007fff`f8609aba     SHELL32!CAutoComplete::_EditWndProc+0xb1
    04 000000c8`2647bde0 00007fff`f86098b7     COMCTL32!CallNextSubclassProc+0x9a
    05 000000c8`2647be60 00007ff8`0782e858     COMCTL32!MasterSubclassProc+0xa7
    06 000000c8`2647bf00 00007ff8`0782de1b     USER32!UserCallWinProcCheckWow+0x2f8
    07 000000c8`2647c090 00007ff8`0782d68a     USER32!SendMessageWorker+0x70b
    08 000000c8`2647c130 00007ff8`07afa4db     USER32!SendMessageW+0xda
    ```

13. 若要退出调试并从记事本进程分离，请输入以下命令：

    [qd](qd--quit-and-detach-.md)

## <a name="launch-your-own-application-and-attach-windbg"></a>启动自己的应用程序并附加 WinDbg

假设你已编写并生成此小型控制台应用程序。

```cpp
...
void MyFunction(long p1, long p2, long p3)
{
    long x = p1 + p2 + p3;
    long y = 0;
    y = x / p2;
}

void main ()
{
    long a = 2;
    long b = 0;
    MyFunction(a, b, 5);
}
```

对于本练习，我们将假设生成的应用程序 (MyApp.exe) 和符号文件 (MyApp.pdb) 位于 C:\\MyApp\\x64\\Debug。 我们还将假设应用程序源代码位于 C:\\MyApp\\MyApp 中，并且目标计算机编译了 MyApp.exe。

1. 打开 WinDbg。

2. 在“文件”菜单上，选择“打开可执行文件”   。 在“打开可执行文件”对话框中，导航到 C:\\MyApp\\x64\\Debug。 输入 MyApp.exe 作为“文件名称”  。 选择“打开”。
3. 输入以下命令：

    [.symfix](-symfix--set-symbol-store-path-.md)

    [.sympath](-sympath--set-symbol-path-.md)+ C:\\MyApp\\x64\\Debug

    现在，WinDbg 知道在何处可以找到应用程序的符号和源代码。 在这种情况下，不需要用 [.srcpath](-srcpath---lsrcpath--set-source-path-.md) 设置源代码位置，因为符号具有指向源文件的完全限定路径。

4. 输入以下命令：

    [.reload](-reload--reload-module-.md)

    [bu MyApp!main](bp--bu--bm--set-breakpoint-.md)

    [g](g--go-.md)

    应用程序在调试器的主函数中中断  。

    WinDbg 显示源代码和命令窗口。

    ![windbg 中源代码的屏幕截图](images/windbggetstart03.png)

5. 在“调试”菜单上，选择“单步调试”（或按“F11”）    。 继续单步调试，直到进入 MyFunction  。 单步调试 `y = x / p2` 行时，应用程序将崩溃并中断到调试器。 输出类似于以下内容：

    ```dbgcmd
    (1450.1424): Integer divide-by-zero - code c0000094 (first chance)
    First chance exceptions are reported before any exception handling.
    This exception may be expected and handled.
    MyApp!MyFunction+0x44:
    00007ff6`3be11064 f77c2428    idiv  eax,dword ptr [rsp+28h] ss:00000063`2036f808=00000000
    ```

6. 输入此命令：

    [!analyze -v](-analyze.md)

    WinDbg 显示问题的分析（在这种情况下除以 0）。

    ```dbgcmd
    FAULTING_IP:
    MyApp!MyFunction+44 [c:\myapp\myapp\myapp.cpp @ 7]
    00007ff6`3be11064 f77c2428        idiv    eax,dword ptr [rsp+28h]

    EXCEPTION_RECORD:  ffffffffffffffff -- (.exr 0xffffffffffffffff)
    ExceptionAddress: 00007ff63be11064 (MyApp!MyFunction+0x0000000000000044)
       ExceptionCode: c0000094 (Integer divide-by-zero)
      ExceptionFlags: 00000000
    NumberParameters: 0
    ...
    STACK_TEXT:  
    00000063`2036f7e0 00007ff6`3be110b8 : ... : MyApp!MyFunction+0x44
    00000063`2036f800 00007ff6`3be1141d : ... : MyApp!main+0x38
    00000063`2036f840 00007ff6`3be1154e : ... : MyApp!__tmainCRTStartup+0x19d
    00000063`2036f8b0 00007ffc`b1cf16ad : ... : MyApp!mainCRTStartup+0xe
    00000063`2036f8e0 00007ffc`b1fc4629 : ... : KERNEL32!BaseThreadInitThunk+0xd
    00000063`2036f910 00000000`00000000 : ... : ntdll!RtlUserThreadStart+0x1d

    STACK_COMMAND: dt ntdll!LdrpLastDllInitializer BaseDllName ;dt ntdll!LdrpFailureData ;.cxr 0x0 ;kb

    FOLLOWUP_IP:
    MyApp!MyFunction+44 [c:\myapp\myapp\myapp.cpp @ 7]
    00007ff6`3be11064 f77c2428        idiv    eax,dword ptr [rsp+28h]

    FAULTING_SOURCE_LINE:  c:\myapp\myapp\myapp.cpp

    FAULTING_SOURCE_FILE:  c:\myapp\myapp\myapp.cpp

    FAULTING_SOURCE_LINE_NUMBER:  7

    FAULTING_SOURCE_CODE:  
         3: void MyFunction(long p1, long p2, long p3)
         4: {
         5:     long x = p1 + p2 + p3;
         6:     long y = 0;
    >    7:  y = x / p2;
         8: }
         9:
        10: void main ()
        11: {
        12:     long a = 2;
    ...
    ```

## <a name="summary-of-commands"></a>命令摘要

- “帮助”菜单上的“内容”命令
- [.sympath（设置符号路径）](-sympath--set-symbol-path-.md)
- [.reload（重新加载模块）](-reload--reload-module-.md)
- [x（检查符号）](x--examine-symbols-.md)
- [g（转到）](g--go-.md)
- 在“调试”菜单上“中断”命令
- [lm（列出已加载的模块）](lm--list-loaded-modules-.md)
- [k（显示堆栈回溯）](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)
- [bu（设置断点）](bp--bu--bm--set-breakpoint-.md)
- [bl（断点列表）](bl--breakpoint-list-.md)
- [~（线程状态）](---thread-status-.md)
- [~s（设置当前线程）](-s--set-current-thread-.md)
- [.sympath+（设置符号路径）附加到现有符号路径](-sympath--set-symbol-path-.md)
- [srcpath（设置源路径）](-srcpath---lsrcpath--set-source-path-.md)
- “调试”菜单上的“单步调试”命令 (F11)
- [!analyze -v](-analyze.md)
- [qd（退出和分离）](qd--quit-and-detach-.md)

## <a name="see-also"></a>另请参阅

[Getting Started with WinDbg (Kernel-Mode)](getting-started-with-windbg--kernel-mode-.md)（WinDbg 入门（内核模式））

[调试程序操作](debugger-operation-win8.md)

[调试方法](debugging-techniques.md)

[Windows 调试工具（WinDbg、KD、CDB、NTSD）](./index.md)

[使用 WinDbg 预览版进行调试](debugging-using-windbg-preview.md)
