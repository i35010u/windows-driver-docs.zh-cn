---
title: DumpChk
description: DumpChk
ms.assetid: f7431207-562b-451a-843e-1c2be038e306
keywords:
- DumpChk
ms.date: 09/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3fbbd46c8ec6c4e361078394f208fc753dc97c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567213"
---
# <a name="dumpchk"></a>DumpChk


DumpChk （Microsoft 崩溃转储文件检查器工具） 是一个可执行的崩溃转储文件的快速分析程序。 这使您可以查看有关转储文件包含摘要信息。 如果转储文件已损坏，无法打开由调试器的方式，dumpchk 将会显示这一事实。

## <a name="span-idwheretogetdumpchkspanspan-idwheretogetdumpchkspanspan-idwheretogetdumpchkspanwhere-to-get-dumpchk"></a><span id="Where_to_get_DumpChk"></span><span id="where_to_get_dumpchk"></span><span id="WHERE_TO_GET_DUMPCHK"></span>从中获取 DumpChk


中包含 DumpChk.exe[有关 Windows 调试工具](index.md)。

## <a name="span-iddumpchkcommand-lineoptionsspanspan-iddumpchkcommand-lineoptionsspanspan-iddumpchkcommand-lineoptionsspandumpchk-command-line-options"></a><span id="DumpChk_command-line_options"></span><span id="dumpchk_command-line_options"></span><span id="DUMPCHK_COMMAND-LINE_OPTIONS"></span>DumpChk 命令行选项


```dbgcmd
DumpChk [-y SymbolPath] DumpFile
```

### <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="_______-y________SymbolPath______"></span><span id="_______-y________symbolpath______"></span><span id="_______-Y________SYMBOLPATH______"></span> **-y** *SymbolPath*   
*SymbolPath*指定 DumpChk 将搜索符号。 符号信息可能需要一些转储文件。 它还有助于提高中显示的信息的转储文件，从而符号名称会得到解决。

<span id="_______DumpFile______"></span><span id="_______dumpfile______"></span><span id="_______DUMPFILE______"></span> *DumpFile*   
*DumpFile*指定要分析的崩溃转储文件。 这可能包括绝对或相对目录路径或通用命名约定 (UNC) 路径。 如果*DumpFile*包含空格，则必须用引号引起来。

## <a name="span-idusingdumpchkspanspan-idusingdumpchkspanspan-idusingdumpchkspanusing-dumpchk"></a><span id="Using_DumpChk"></span><span id="using_dumpchk"></span><span id="USING_DUMPCHK"></span>使用 DumpChk


下面是的示例中的转储文件已损坏。 在结束时，显示的错误`DebugClient cannot open DumpFile`，指示必须具有发生某种类型的损坏：

```console
C:\Debuggers> dumpchk c:\mydir\dumpfile2.dmp 

Loading dump file c:\mydir\dumpfile2.dmp

Microsoft (R) Windows Debugger Version 6.9.0003.113 X86
Copyright (C) Microsoft. All rights reserved.


Loading Dump File [c:\mydir\dumpfile2.dmp]
Could not match Dump File signature - invalid file format
Could not open dump file [c:\mydir\dumpfile2.dmp], HRESULT 0x80004002
    "No such interface supported"
**** DebugClient cannot open DumpFile - error 80004002   
```

因为此显示不会结束的单词`Finished dump check`，转储文件已损坏。 结束时的错误消息说明无法打开转储文件。

请注意，可能会列出其他错误，其中一些实际良性。 例如，以下错误消息不表示问题：

```dbgcmd
error 3 InitTypeRead( nt!_PEB at 7ffd5000) 
```

下面是 DumpChk 正常用户模式小型转储上运行的示例。 显示开始转储文件的总体摘要，然后提供了有关转储文件中包含的数据时的详细的信息：

```console
C:\Debuggers> dumpchk c:\mydir\dumpfile1.dmp 

Loading dump file c:\mydir\dumpfile1.dmp

Microsoft (R) Windows Debugger Version 6.9.0003.113 X86
Copyright (C) Microsoft. All rights reserved.


Loading Dump File [c:\mydir\dumpfile1.dmp]
User Mini Dump File with Full Memory: Only application data is available

Symbol search path is: srv*C:\CODE\LocalStore*\\symbols\symbols
Executable search path is: 
Windows Vista Version 6000 MP (2 procs) Free x86 compatible
Product: WinNt, suite: SingleUserTS
Debug session time: Tue Jun 17 02:28:23.000 2008 (GMT-7)
System Uptime: 0 days 15:43:52.861
Process Uptime: 0 days 0:00:26.000
...
This dump file has an exception of interest stored in it.
The stored exception information can be accessed via .ecxr.

----- User Mini Dump Analysis

MINIDUMP_HEADER:
Version         A793 (6903)
NumberOfStreams 12
Flags           1826
                0002 MiniDumpWithFullMemory
                0004 MiniDumpWithHandleData
                0020 MiniDumpWithUnloadedModules
                0800 MiniDumpWithFullMemoryInfo
                1000 MiniDumpWithThreadInfo

Streams:
Stream 0: type ThreadListStream (3), size 00000064, RVA 000001BC
  2 threads
  RVA 000001C0, ID 1738, Teb:000000007FFDF000
  RVA 000001F0, ID 1340, Teb:000000007FFDE000
Stream 1: type ThreadInfoListStream (17), size 0000008C, RVA 00000220
  RVA 0000022C, ID 1738
  RVA 0000026C, ID 1340
Stream 2: type ModuleListStream (4), size 00000148, RVA 000002AC
  3 modules
  RVA 000002B0, 00400000 - 00438000: 'C:\CODE\TimeTest\Debug\TimeTest.exe'
  RVA 0000031C, 779c0000 - 77ade000: 'C:\Windows\System32\ntdll.dll'
  RVA 00000388, 76830000 - 76908000: 'C:\Windows\System32\kernel32.dll'
Stream 3: type Memory64ListStream (9), size 00000290, RVA 00001D89
  40 memory ranges
  RVA 0x2019 BaseRva
  range#    RVA      Address      Size
       0 00002019    00010000   00010000
       1 00012019    00020000   00005000
       2 00017019    0012e000   00002000

 (additional stream data deleted)   

Stream 9: type UnusedStream (0), size 00000000, RVA 00000000
Stream 10: type UnusedStream (0), size 00000000, RVA 00000000
Stream 11: type UnusedStream (0), size 00000000, RVA 00000000


Windows Vista Version 6000 MP (2 procs) Free x86 compatible
Product: WinNt, suite: SingleUserTS
kernel32.dll version: 6.0.6000.16386 (vista_rtm.061101-2205)
Debug session time: Tue Jun 17 02:28:23.000 2008 (GMT-7)
System Uptime: 0 days 15:43:52.861
Process Uptime: 0 days 0:00:26.000
  Kernel time: 0 days 0:00:00.000
  User time: 0 days 0:00:00.000
PEB at 7ffd9000
    InheritedAddressSpace:    No
    ReadImageFileExecOptions: No
    BeingDebugged:            Yes
    ImageBaseAddress:         00400000
    Ldr                       77a85d00
    Ldr.Initialized:          Yes
    Ldr.InInitializationOrderModuleList: 002c1e30 . 002c2148
    Ldr.InLoadOrderModuleList:           002c1da0 . 002c2138
    Ldr.InMemoryOrderModuleList:         002c1da8 . 002c2140
            Base TimeStamp                     Module
          400000 47959d85 Jan 21 23:38:45 2008 C:\CODE\TimeTest\Debug\TimeTest.exe
        779c0000 4549bdc9 Nov 02 02:43:37 2006 C:\Windows\system32\ntdll.dll
        76830000 4549bd80 Nov 02 02:42:24 2006 C:\Windows\system32\kernel32.dll
    SubSystemData:     00000000
    ProcessHeap:       002c0000
    ProcessParameters: 002c14c0
    WindowTitle:  'C:\CODE\TimeTest\Debug\TimeTest.exe'
    ImageFile:    'C:\CODE\TimeTest\Debug\TimeTest.exe'
    CommandLine:  '\CODE\TimeTest\Debug\TimeTest.exe'
    DllPath:      'C:\CODE\TimeTest\Debug;C:\Windows\system32;C:\Windows\system;
    Environment:  002c0808
        =C:=C:\CODE
        =ExitCode=00000000
        ALLUSERSPROFILE=C:\ProgramData
        AVENGINE=C:\PROGRA~1\CA\SHARED~1\SCANEN~1
        CommonProgramFiles=C:\Program Files\Common Files
        COMPUTERNAME=EMNET
        ComSpec=C:\Windows\system32\cmd.exe
        configsetroot=C:\Windows\ConfigSetRoot
        FP_NO_HOST_CHECK=NO
        HOMEDRIVE=C:
        NUMBER_OF_PROCESSORS=2
        OS=Windows_NT
        Path=C:\DTFW\200804~2.113\winext\arcade;C:\Windows\system32
        PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
        PROCESSOR_ARCHITECTURE=x86
        PROCESSOR_IDENTIFIER=x86 Family 6 Model 15 Stepping 13, GenuineIntel
        PROCESSOR_LEVEL=6
        PROCESSOR_REVISION=0f0d
        ProgramData=C:\ProgramData
        ProgramFiles=C:\Program Files
        PROMPT=$P$G
        PUBLIC=C:\Users\Public
        RoxioCentral=C:\Program Files\Common Files\Roxio Shared\9.0\Roxio Central33\
        SESSIONNAME=Console
        SystemDrive=C:
        SystemRoot=C:\Windows
        USERDNSDOMAIN=NORTHSIDE.COMPANY.COM
        USERDOMAIN=NORTHSIDE
        USERNAME=myname
        USERPROFILE=C:\Users\myname
        WINDBG_DIR=C:\DTFW\200804~2.113
        windir=C:\Windows
        WINLAYTEST=200804~2.113
        _NT_SOURCE_PATH=C:\mysources
        _NT_SYMBOL_PATH=C:\mysymbols
Finished dump check
```

在输出开始通过标识转储文件-在这种情况下，使用完整的内存信息，包括应用程序数据，但不是操作系统的数据包括用户模式下小型转储的特征。 这被跟正由 DumpChk，，然后选择转储文件内容的摘要的符号路径。

因为此显示结尾单词`Finished dump check`，转储文件可能不是已损坏，并可由调试器打开。 但是，corrruption 的更多细微的窗体仍可能会出现在该文件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 调试工具中包含的工具](extra-tools.md)

 

 






