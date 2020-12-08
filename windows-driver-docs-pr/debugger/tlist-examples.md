---
title: TList 示例
description: TList 示例
keywords:
- Tlist.exe，Tlist.exe 示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 535c04d76d5aeb6e14261ff71f328e40aa0e9481
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801877"
---
# <a name="tlist-examples"></a>TList 示例


## <span id="ddk_tlist_examples_dtools"></span><span id="DDK_TLIST_EXAMPLES_DTOOLS"></span>


下面的示例演示如何使用 Tlist.exe。

### <a name="span-idsimplest_tlist_command__tlist_spanspan-idsimplest_tlist_command__tlist_spansimplest-tlist-command-tlist"></a><span id="simplest_tlist_command__tlist_"></span><span id="SIMPLEST_TLIST_COMMAND__TLIST_"></span>最简单的 Tlist.exe 命令 (tlist.exe) 

键入不带其他参数的 **tlist.exe** 将显示正在运行的进程的列表、其进程 Id (pid) ，以及运行它们的窗口的标题（如果有）。

```console
c:\>tlist

   0 System Process  
   4 System          
 308 smss.exe        
 356 csrss.exe         
 380 winlogon.exe      NetDDE Agent
 424 services.exe    
 436 lsass.exe       
 604 svchost.exe     
 776 svchost.exe     
 852 spoolsv.exe     
1000 clisvcl.exe     
1036 InoRpc.exe      
1064 InoRT.exe       
1076 InoTask.exe     
1244 WTTSvc.exe        
1492 Sysparse_com.exe  OleMainThreadWndName
1980 explorer.exe      Program Manager
1764 launch32.exe      SMS Client User Application Launcher 
1832 msmsgs.exe        MSBLNetConn
2076 ctfmon.exe        
2128 ISATRAY.EXE       IsaTray
4068 tlist.exe   
```

### <a name="span-idfind_a_process_id___p_spanspan-idfind_a_process_id___p_spanfind-a-process-id--p"></a><span id="find_a_process_id___p_"></span><span id="FIND_A_PROCESS_ID___P_"></span>查找进程 ID (-p) 

以下命令使用 **-p** 参数和进程名称查找 Explorer.exe (资源管理器) 进程的进程 ID。

在响应中，Tlist.exe 显示资源管理器进程的进程 ID 328。

```console
c:\>tlist -p explorer
328
```

### <a name="span-idfind_process_details_using_pidspanspan-idfind_process_details_using_pidspanfind-process-details-using-pid"></a><span id="find_process_details_using_pid"></span><span id="FIND_PROCESS_DETAILS_USING_PID"></span>使用 PID 查找进程详细信息

以下命令使用资源管理器运行的进程的进程 ID 查找有关资源管理器进程的详细信息。

```console
c:\>tlist 328
```

在响应中，Tlist.exe 显示资源管理器进程的详细信息，包括以下元素：

-   进程 ID、可执行文件名称、程序友好名称。

-   当前工作目录 (CWD) 。

-   启动进程的命令行 (CmdLine) 。

-   当前虚拟地址空间值。

-   线程数。

-   进程中运行的线程的列表。 对于每个线程，Tlist.exe 将显示线程 ID (TID) 、线程正在运行的函数、入口点的地址、上次报告的错误的地址 (if 任何) 和线程状态。

-   为进程加载的模块的列表。 对于每个模块，Tlist.exe 将显示模块的版本号、属性、虚拟地址和模块名称。

下面是此命令生成的输出摘录。

```console
 328 explorer.exe      Program Manager
   CWD:     C:\Documents and Settings\user01\
   CmdLine: C:\WINDOWS\Explorer.EXE
   VirtualSize:    90120 KB   PeakVirtualSize:   104844 KB
   WorkingSetSize: 19676 KB   PeakWorkingSetSize: 35716 KB
   NumberOfThreads: 17
    332 Win32StartAddr:0x010160cc LastErr:0x00000008 State:Waiting
   1232 Win32StartAddr:0x70a7def2 LastErr:0x00000000 State:Waiting
   1400 Win32StartAddr:0x77f883de LastErr:0x00000000 State:Waiting
   1452 Win32StartAddr:0x77f91e38 LastErr:0x00000000 State:Waiting
   1484 Win32StartAddr:0x70a7def2 LastErr:0x00000006 State:Waiting
   1904 Win32StartAddr:0x74b02ed6 LastErr:0x00000000 State:Ready
   1948 Win32StartAddr:0x72d22ecc LastErr:0x00000000 State:Waiting
   ....  (thread data deleted here)

  6.0.2800.1106 shp  0x01000000  Explorer.EXE
  5.1.2600.1217 shp  0x77F50000  ntdll.dll
  5.1.2600.1106 shp  0x77E60000  kernel32.dll
  7.0.2600.1106 shp  0x77C10000  msvcrt.dll
  5.1.2600.1106 shp  0x77DD0000  ADVAPI32.dll
  5.1.2600.1254 shp  0x78000000  RPCRT4.dll
  5.1.2600.1106 shp  0x77C70000  GDI32.dll
  5.1.2600.1255 shp  0x77D40000  USER32.dll
  ....  (module data deleted here)
```

### <a name="span-idfind_multiple_processes__pattern_spanspan-idfind_multiple_processes__pattern_spanfind-multiple-processes-pattern"></a><span id="find_multiple_processes__pattern_"></span><span id="FIND_MULTIPLE_PROCESSES__PATTERN_"></span> (模式找到多个进程) 

下面的命令通过表示一个或多个进程的进程名称或窗口名称的正则表达式搜索进程。 在此示例中，该命令将搜索进程名称或窗口名称以 "app.ino" 开头的进程。

```console
c:\>tlist ino*
```

在响应中，Tlist.exe 显示 Inorpc.exe、Inort.exe 和 Inotask.exe 的进程详细信息。 有关输出的说明，请参阅上面的 "使用 PID 查找进程详细信息" 小节。

### <a name="span-iddisplay_a_process_tree___t_spanspan-iddisplay_a_process_tree___t_spandisplay-a-process-tree-t"></a><span id="display_a_process_tree___t_"></span><span id="DISPLAY_A_PROCESS_TREE___T_"></span>显示进程树 (/t) 

以下命令显示一个树，该树表示在计算机上运行的进程。 进程显示为创建它们的进程的子项。

```console
c:\>tlist /t
```

生成的进程树如下所示。 此树显示了系统 (4) 进程创建的 Smss.exe 进程，该进程创建 Csrss.exe、Winlogon.exe、Lsass.exe 和 Rundll32.exe。 此外，Winlogon.exe 创建 Services.exe，这会创建与服务相关的所有过程。

```console
System Process (0)
System (4)
  smss.exe (404)
    csrss.exe (452)
    winlogon.exe (476) NetDDE Agent
      services.exe (520)
        svchost.exe (700)
        svchost.exe (724)
        svchost.exe (864)
        svchost.exe (888)
        spoolsv.exe (996)
        scardsvr.exe (1040)
        alg.exe (1172)
        atievxx.exe (1200) ATI video bios poller
        InoRpc.exe (1248)
        InoRT.exe (1264)
        InoTask.exe (1308)
        mdm.exe (1392)
        dllhost.exe (2780)
      lsass.exe (532)
      rundll32.exe (500)
explorer.exe (328) Program Manager
  WLANMON.exe (1728) TI Wireless LAN Monitor
  ISATRAY.EXE (1712) IsaTray
  cmmon32.exe (456)
  WINWORD.EXE (844) Tlist.doc - Microsoft Word
  dexplore.exe (2096) Platform SDK - CreateThread
```

### <a name="span-idfind_process_by_module___m_spanspan-idfind_process_by_module___m_spanfind-process-by-module-m"></a><span id="find_process_by_module___m_"></span><span id="FIND_PROCESS_BY_MODULE___M_"></span>按模块 (/m 查找进程) 

以下命令将查找在加载特定 DLL 的计算机上运行的所有进程。

```console
c:\>tlist /m 
```

在响应中，Tlist.exe 显示 Inorpc.exe、Inort.exe 和 Inotask.exe 的进程详细信息。 有关输出的说明，请参阅上面的 "使用 PID 查找进程详细信息" 小节。

 

 





