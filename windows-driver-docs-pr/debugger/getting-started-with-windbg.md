---
title: WinDbg 入门（用户模式）
description: WinDbg 是一个内核模式和用户模式下的调试器所包含的 Windows 调试工具。 此处我们提供了实际操作相关的练习，将帮助你开始使用 WinDbg 作为用户模式下调试程序。
ms.assetid: 8C2D2D0C-7E54-4711-A6FD-970E040F1C50
ms.date: 10/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09ff070bc8b49a8851b17c25988435b03866e37b
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866531"
---
# <a name="getting-started-with-windbg-user-mode"></a>WinDbg 入门（用户模式）

WinDbg 是一个内核模式和用户模式下的调试器所包含的 Windows 调试工具。 此处我们提供了实际操作相关的练习，将帮助你开始使用 WinDbg 作为用户模式下调试程序。

有关如何获取有关 Windows 调试工具的信息，请参阅[调试工具的 Windows （WinDbg、 KD、 CDB、 NTSD）](https://go.microsoft.com/fwlink/p?linkid=223405)。 

已安装调试工具后，找到 (x64) 64 位和 32 位 (x86) 版本的工具的安装目录。 例如：

-   C:\\程序文件 (x86)\\Windows 工具包\\8.1\\调试器\\x64
-   C:\\程序文件 (x86)\\Windows 工具包\\8.1\\调试器\\x86

## <a name="span-idlaunchnotepadandattachwindbgspanspan-idlaunchnotepadandattachwindbgspanspan-idlaunchnotepadandattachwindbgspanlaunch-notepad-and-attach-windbg"></a><span id="Launch_Notepad_and_attach_WinDbg"></span><span id="launch_notepad_and_attach_windbg"></span><span id="LAUNCH_NOTEPAD_AND_ATTACH_WINDBG"></span>启动记事本并将 WinDbg 附加

1.  导航到安装目录，并打开 WinDbg.exe。

2.  调试程序文档，还可以在行[此处](https://go.microsoft.com/fwlink/p?linkid=223405)。

3.  上**文件**菜单中，选择**打开可执行文件**。 在打开可执行文件对话框中，导航到包含 notepad.exe 的文件夹 (例如，c:\\Windows\\System32)。 有关**文件名**，输入 notepad.exe。 单击“打开”  。

    ![启动记事本后的 windbg 的屏幕截图](images/windbggetstart01.png)

4.  靠近底部 WinDbg 窗口中，在命令行中，输入以下命令：

    [.sympath srv\*](https://go.microsoft.com/fwlink/p?linkid=399238)

    输出结果类似于此：

    ```dbgcmd
    Symbol search path is: srv*
    Expanded Symbol search path is: cache*;SRV
    ```

    符号搜索路径告知 WinDbg 查找符号 (PDB) 文件的位置。 调试器需要符号文件，以了解有关代码模块 （函数名称、 变量名称等） 的信息。

    请输入以下命令，它会告知 WinDbg，执行其初始查找和加载的符号文件：

    [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)

5.  若要查看 Notepad.exe 模块的符号，输入以下命令：

    [x 记事本 ！ *](https://go.microsoft.com/fwlink/p?linkid=399240)

    **请注意**  如果你看不到任何输出，请输入[ **.reload** ](https://go.microsoft.com/fwlink/p?linkid=399239)试。

    若要查看包含主 Notepad.exe 模块中的符号，输入以下命令：

    [x 记事本 ！\*主要\*](https://go.microsoft.com/fwlink/p?linkid=399240)
 
    输出结果类似于此：

    ```dbgcmd
    000000d0`428ff7e8 00007ff6`3282122f notepad!WinMain
    ...
    ```

6.  若要将断点放在记事本 ！WinMain，输入以下命令：

    [bu notepad!WinMain](https://go.microsoft.com/fwlink/p?linkid=399390)

    若要验证已设置了断点，请输入以下命令：

    [bl](https://go.microsoft.com/fwlink/p?linkid=399391)

    输出结果类似于此：

    ```dbgcmd
    0 e 00007ff6`32825f64     0001 (0001)  0:**** notepad!WinMain
    ```

7.  若要开始运行记事本，输入以下命令：

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

    记事本一直运行，直到进入**WinMain**函数，并且到调试器中的然后中断。

    若要查看的记事本进程中加载的代码模块的列表，请输入以下命令：

    [lm](https://go.microsoft.com/fwlink/p?linkid=399237)

    输出结果类似于此：

    ```dbgcmd
    0:000> lm
    start             end                 module name
    00007ff6`32820000 00007ff6`3285a000   notepad    (pdb symbols)          C:\...\notepad.pdb
    00007ffc`ab7e0000 00007ffc`ab85b000   WINSPOOL   (deferred)             
    00007ffc`aba10000 00007ffc`abc6a000   COMCTL32   (deferred)             
    00007ffc`adea0000 00007ffc`adf3f000   SHCORE     (deferred)             
    00007ffc`af490000 00007ffc`af59f000   KERNELBASE   (deferred)             
    00007ffc`af7d0000 00007ffc`af877000   msvcrt     (deferred)             
    00007ffc`af880000 00007ffc`b0c96000   SHELL32    (deferred)             
    00007ffc`b0e40000 00007ffc`b0ef7000   OLEAUT32   (deferred)             
    00007ffc`b0f00000 00007ffc`b0f57000   sechost    (deferred)             
    00007ffc`b0f60000 00007ffc`b1005000   ADVAPI32   (deferred)             
    00007ffc`b1010000 00007ffc`b1155000   GDI32      (deferred)             
    00007ffc`b1160000 00007ffc`b1296000   RPCRT4     (deferred)             
    00007ffc`b12a0000 00007ffc`b1411000   USER32     (deferred)             
    00007ffc`b1420000 00007ffc`b15f6000   combase    (deferred)             
    00007ffc`b16c0000 00007ffc`b17f9000   MSCTF      (deferred)             
    00007ffc`b1800000 00007ffc`b189a000   COMDLG32   (deferred)             
    00007ffc`b18a0000 00007ffc`b18f1000   SHLWAPI    (deferred)             
    00007ffc`b1b60000 00007ffc`b1cd8000   ole32      (deferred)             
    00007ffc`b1cf0000 00007ffc`b1e2a000   KERNEL32   (pdb symbols)          C:\...\kernel32.pdb
    00007ffc`b1eb0000 00007ffc`b1ee4000   IMM32      (deferred)             
    00007ffc`b1f50000 00007ffc`b20fa000   ntdll      (private pdb symbols)  C:\...\ntdll.pdb
    ```

    若要查看堆栈跟踪，请输入以下命令：

    [k](https://go.microsoft.com/fwlink/p?linkid=399389)

    输出结果类似于此：

    ```dbgcmd
    Breakpoint 0 hit
    notepad!WinMain:
    00007ff6`32825f64 488bc4          mov     rax,rsp
    0:000> k
    Child-SP          RetAddr           Call Site
    00000048`4e0cf6a8 00007ff6`3282122f notepad!WinMain
    00000048`4e0cf6b0 00007ffc`b1cf16ad notepad!WinMainCRTStartup+0x1a7
    00000048`4e0cf770 00007ffc`b1fc4629 KERNEL32!BaseThreadInitThunk+0xd
    00000048`4e0cf7a0 00000000`00000000 ntdll!RtlUserThreadStart+0x1d ...
    ```

8.  若要开始再次运行记事本，输入以下命令：

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

9.  若要中断到记事本，请选择**中断**从**调试**菜单。

10. 若要设置并验证在断点**ZwWriteFile**，输入以下命令：

    [bu ntdll!ZwWriteFile](https://go.microsoft.com/fwlink/p?linkid=399390)

    [bl](https://go.microsoft.com/fwlink/p?linkid=399391)

11. 输入[g](https://go.microsoft.com/fwlink/p?linkid=399388)以启动记事本再次运行。 在记事本窗口中，输入一些文本，然后选择**保存**从**文件**菜单。 在涉及到正在运行的代码分隔线**zwcreatefile 转换**。 输入[k](https://go.microsoft.com/fwlink/p?linkid=399389)以查看堆栈跟踪。

    ![在 windbg 中的堆栈跟踪的屏幕截图](images/windbggetstart02.png)

    在 WinDbg 窗口中的命令行的左侧，可以看到的处理器和线程的编号。 在此示例中当前的处理器数为 0，并且当前的线程数为 11。 因此，我们正在查看堆栈跟踪的线程 11 （它碰巧在处理器 0 上运行）。

12. 若要查看 Notepad 进程中所有线程的列表，请输入此命令 （波形符）：

    [~](https://go.microsoft.com/fwlink/p?linkid=399392)

    输出结果类似于此：

    ```dbgcmd
    0:011> ~
       0  Id: 10c8.128c Suspend: 1 Teb: 00007ff6`31cdd000 Unfrozen
       1  Id: 10c8.1a10 Suspend: 1 Teb: 00007ff6`31cdb000 Unfrozen
       2  Id: 10c8.1850 Suspend: 1 Teb: 00007ff6`31cd9000 Unfrozen
       3  Id: 10c8.1774 Suspend: 1 Teb: 00007ff6`31cd7000 Unfrozen
       4  Id: 10c8.1e80 Suspend: 1 Teb: 00007ff6`31cd5000 Unfrozen
       5  Id: 10c8.10ac Suspend: 1 Teb: 00007ff6`31cd3000 Unfrozen
       6  Id: 10c8.13a4 Suspend: 1 Teb: 00007ff6`31bae000 Unfrozen
       7  Id: 10c8.2b4 Suspend: 1 Teb: 00007ff6`31bac000 Unfrozen
       8  Id: 10c8.1df0 Suspend: 1 Teb: 00007ff6`31baa000 Unfrozen
       9  Id: 10c8.1664 Suspend: 1 Teb: 00007ff6`31ba8000 Unfrozen
      10  Id: 10c8.15e4 Suspend: 1 Teb: 00007ff6`31ba6000 Unfrozen
    . 11  Id: 10c8.8bc Suspend: 1 Teb: 00007ff6`31ba4000 Unfrozen
    ```

    在此示例中，有 12 个线程索引为 0 到 11。

13. 若要查看线程的堆栈跟踪，请输入以下命令：

    [~0s](https://go.microsoft.com/fwlink/p?linkid=399393)

    [k](https://go.microsoft.com/fwlink/p?linkid=399389)

    输出结果类似于此：

    ```dbgcmd
    0:011> ~0s
    USER32!SystemParametersInfoW:
    00007ffc`b12a4d20 48895c2408      mov     qword ptr [rsp+8], ...
    0:000> k
    Child-SP          RetAddr           Call Site
    00000033`d1e9da48 00007ffc`adfb227d USER32!SystemParametersInfoW
    (Inline Function) --------`-------- uxtheme!IsHighContrastMode+0x1d
    00000033`d1e9da50 00007ffc`adfb2f12 uxtheme!IsThemeActive+0x4d
    ...
    00000033`d1e9f810 00007ffc`b1cf16ad notepad!WinMainCRTStartup+0x1a7
    00000033`d1e9f8d0 00007ffc`b1fc4629 KERNEL32!BaseThreadInitThunk+0xd
    00000033`d1e9f900 00000000`00000000 ntdll!RtlUserThreadStart+0x1d
    ```

14. 若要退出调试，并从记事本的进程分离，输入以下命令：

    [qd](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idlaunchyourownapplicationandattachwindbgspanspan-idlaunchyourownapplicationandattachwindbgspanspan-idlaunchyourownapplicationandattachwindbgspanlaunch-your-own-application-and-attach-windbg"></a><span id="Launch_your_own_application_and_attach_WinDbg"></span><span id="launch_your_own_application_and_attach_windbg"></span><span id="LAUNCH_YOUR_OWN_APPLICATION_AND_ATTACH_WINDBG"></span>启动自己的应用程序和附加 WinDbg


假设你已编写和构建此小型控制台应用程序。

```dbgcmd
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

对于此练习中，我们将假定生成的应用程序 (MyApp.exe) 和符号文件 (MyApp.pdb) 位于 c:\\MyApp\\x64\\调试。 我们还假设 c： 驱动器中为应用程序源代码\\MyApp\\MyApp 和目标计算机编译 MyApp.exe。

1.  打开 WinDbg。

2.  上**文件**菜单中，选择**打开可执行文件**。 在打开可执行文件对话框中，导航到 c:\\MyApp\\x64\\调试。 有关**文件名**，输入 MyApp.exe。 单击“打开”  。
3.  输入以下命令：

    [.symfix](https://docs.microsoft.com/windows-hardware/drivers/debugger/-symfix--set-symbol-store-path-)

    [.sympath](https://docs.microsoft.com/windows-hardware/drivers/debugger/-sympath--set-symbol-path-)+ c:\\MyApp\\x64\\调试

    现在 WinDbg 知道在哪里可以找到你的应用程序的符号和源代码。 在这种情况下，源代码位置不需要用来设置[.srcpath](https://docs.microsoft.com/windows-hardware/drivers/debugger/-srcpath---lsrcpath--set-source-path-)因为符号具有完全限定的源代码文件的路径。

4.  输入以下命令：

    [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)

    [bu MyApp!main](https://go.microsoft.com/fwlink/p?linkid=399390)

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

    你的应用程序在中中断到调试器时涉及到其**主要**函数。

    WinDbg 显示你的源代码和命令窗口。

    ![在 windbg 中的源代码的屏幕截图](images/windbggetstart03.png)

5.  上**调试**菜单中，选择**单步执行**(或按**F11**)。 继续单步执行之前已单步执行**MyFunction**。 当单步执行该行`y = x / p2`，应用程序崩溃和中断到调试器。 输出结果类似于此：

    ```dbgcmd
    (1450.1424): Integer divide-by-zero - code c0000094 (first chance)
    First chance exceptions are reported before any exception handling.
    This exception may be expected and handled.
    MyApp!MyFunction+0x44:
    00007ff6`3be11064 f77c2428    idiv  eax,dword ptr [rsp+28h] ss:00000063`2036f808=00000000
    ```

6.  输入此命令：

    [!analyze -v](https://go.microsoft.com/fwlink/p?linkid=399396)

    WinDbg 显示分析的问题 （被 0 除在此情况下）。

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

## <a name="span-idsummaryofcommandsspanspan-idsummaryofcommandsspanspan-idsummaryofcommandsspansummary-of-commands"></a><span id="Summary_of_commands"></span><span id="summary_of_commands"></span><span id="SUMMARY_OF_COMMANDS"></span>命令摘要


-   **内容**命令**帮助**菜单
-   [.sympath （设置符号路径）](https://go.microsoft.com/fwlink/p?linkid=399238)
-   [.reload （重新加载模块）](https://go.microsoft.com/fwlink/p?linkid=399239)
-   [x （检查符号）](https://go.microsoft.com/fwlink/p?linkid=399240)
-   [g (Go)](https://go.microsoft.com/fwlink/p?linkid=399388)
-   **中断**命令**调试**菜单
-   [lm （列出已加载的模块）](https://go.microsoft.com/fwlink/p?linkid=399237)
-   [k （显示堆栈回溯）](https://go.microsoft.com/fwlink/p?linkid=399389)
-   [bu (Set Breakpoint)](https://go.microsoft.com/fwlink/p?linkid=399390)
-   [bl （断点列表）](https://go.microsoft.com/fwlink/p?linkid=399390)
-   [~ （线程状态）](https://go.microsoft.com/fwlink/p?linkid=399392)
-   [~ s （设置当前线程）](https://go.microsoft.com/fwlink/p?linkid=399393)
-   [.sympath + （设置符号路径） 追加到现有的符号路径](https://go.microsoft.com/fwlink/p?linkid=399238)
-   [.srcpath (Set Source Path)](https://go.microsoft.com/fwlink/p?linkid=399395)
-   **单步执行**命令**调试**菜单 (**F11**)
-   [!analyze -v](https://go.microsoft.com/fwlink/p?linkid=399396)
-   [qd （Quit 和分离）](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Getting Started with WinDbg (Kernel-Mode)](getting-started-with-windbg--kernel-mode-.md)（WinDbg 入门（内核模式））

[调试程序操作](https://go.microsoft.com/fwlink/p?linkid=399247)

[调试方法](https://go.microsoft.com/fwlink/p?linkid=399248)

[（WinDbg、 KD、 CDB、 NTSD） 的 Windows 调试工具](https://go.microsoft.com/fwlink/p?linkid=223405)

 

 






