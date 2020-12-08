---
title: DumpChk
description: DumpChk
keywords:
- DumpChk
ms.date: 09/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfcff2afc8c886cbedfdda1089aaf5192366c028
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838657"
---
# <a name="dumpchk"></a>DumpChk


DumpChk (Microsoft 崩溃转储文件检查器工具) 是对故障转储文件执行快速分析的程序。 这使你可以查看有关转储文件所包含内容的摘要信息。 如果转储文件损坏，导致调试器无法打开该文件，DumpChk 将显示这一事实。

## <a name="span-idwhere_to_get_dumpchkspanspan-idwhere_to_get_dumpchkspanspan-idwhere_to_get_dumpchkspanwhere-to-get-dumpchk"></a><span id="Where_to_get_DumpChk"></span><span id="where_to_get_dumpchk"></span><span id="WHERE_TO_GET_DUMPCHK"></span>从何处获取 DumpChk


DumpChk.exe 包含在 [Windows 调试工具](index.md)中。

## <a name="span-iddumpchk_command-line_optionsspanspan-iddumpchk_command-line_optionsspanspan-iddumpchk_command-line_optionsspandumpchk-command-line-options"></a><span id="DumpChk_command-line_options"></span><span id="dumpchk_command-line_options"></span><span id="DUMPCHK_COMMAND-LINE_OPTIONS"></span>DumpChk 命令行选项


```dbgcmd
DumpChk [-y SymbolPath] DumpFile
```

### <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______-y________SymbolPath______"></span><span id="_______-y________symbolpath______"></span><span id="_______-Y________SYMBOLPATH______"></span>**-y** *SymbolPath*   
*SymbolPath* 指定 DumpChk 搜索符号的位置。 某些转储文件可能需要符号信息。 它还可以通过允许解析符号名称来改善转储文件中显示的信息。

<span id="_______DumpFile______"></span><span id="_______dumpfile______"></span><span id="_______DUMPFILE______"></span>*DumpFile*   
*DumpFile* 指定要分析的故障转储文件。 这可能包括绝对或相对目录路径或通用命名约定 (UNC) 路径。 如果 *DumpFile* 包含空格，则必须用引号将其引起来。

## <a name="span-idusing_dumpchkspanspan-idusing_dumpchkspanspan-idusing_dumpchkspanusing-dumpchk"></a><span id="Using_DumpChk"></span><span id="using_dumpchk"></span><span id="USING_DUMPCHK"></span>使用 DumpChk


下面是转储文件损坏的示例。 最后显示的错误 `DebugClient cannot open DumpFile` 指示必须发生某种类型的损坏：

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

因为此显示不以单词结尾，所以 `Finished dump check` 转储文件已损坏。 最后的错误消息说明无法打开转储文件。

请注意，可能会列出其他错误，其中一些错误实际上是良性的。 例如，以下错误消息不代表问题：

```dbgcmd
error 3 InitTypeRead( nt!_PEB at 7ffd5000) 
```

下面是在正常的用户模式小型转储中运行的 DumpChk 的示例。 此显示从转储文件的总体摘要开始，并提供有关转储文件中包含的数据的详细信息：

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

输出首先标识转储文件的特征-在本例中，是一种包含完整内存信息的用户模式小型转储，其中包括应用程序数据，但不包括操作系统数据。 后跟 DumpChk 使用的符号路径，然后是转储文件内容的摘要。

因为此显示以单词结尾 `Finished dump check` ，所以转储文件可能未损坏，并可由调试程序打开。 但是，corrruption 中的更多微妙形式可能仍然存在于文件中。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 调试工具中包含的工具](extra-tools.md)

 

 






