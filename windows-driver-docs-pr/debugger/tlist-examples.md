---
title: TList 示例
description: TList 示例
ms.assetid: 9c9a1e81-03c2-4b7c-b0da-b25942548aa9
keywords:
- TList，TList 示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d1f614e364bd4a576e2df44c825a2aa1713b8d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524034"
---
# <a name="tlist-examples"></a>TList 示例


## <span id="ddk_tlist_examples_dtools"></span><span id="DDK_TLIST_EXAMPLES_DTOOLS"></span>


以下示例演示如何使用 TList。

### <a name="span-idsimplesttlistcommandtlistspanspan-idsimplesttlistcommandtlistspansimplest-tlist-command-tlist"></a><span id="simplest_tlist_command__tlist_"></span><span id="SIMPLEST_TLIST_COMMAND__TLIST_"></span>最简单 TList 命令 (tlist)

键入**tlist**没有其他参数显示如果任何正在运行进程、 其进程 Id (Pid)，并在其中运行它们，窗口的标题的列表。

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

### <a name="span-idfindaprocessidpspanspan-idfindaprocessidpspanfind-a-process-id--p"></a><span id="find_a_process_id___p_"></span><span id="FIND_A_PROCESS_ID___P_"></span>查找进程 ID (-p)

下面的命令使用 **-p**参数和进程名称，用于确定 Explorer.exe （资源管理器） 进程的进程 ID。

在响应中，TList 显示资源管理器的进程，328 的进程 ID。

```console
c:\>tlist -p explorer
328
```

### <a name="span-idfindprocessdetailsusingpidspanspan-idfindprocessdetailsusingpidspanfind-process-details-using-pid"></a><span id="find_process_details_using_pid"></span><span id="FIND_PROCESS_DETAILS_USING_PID"></span>查找使用 PID 的进程详细信息

以下命令使用资源管理器正在运行，查找有关资源管理器过程的详细的信息的进程的进程 ID。

```console
c:\>tlist 328
```

在响应中，TList 显示资源管理器过程包括以下元素的详细信息：

-   进程 ID，可执行文件名称、 程序友好名称。

-   当前工作目录 (CWD)。

-   命令行启动进程 （命令行）。

-   当前虚拟地址空间值。

-   线程数。

-   在进程中运行的线程的列表。 对于每个线程，TList 显示线程 ID (TID)，运行该线程的函数、 入口点的地址、 地址 （如果有） 的最后一个报告的错误，以及线程状态。

-   为进程加载的模块的列表。 对于每个模块，TList 显示版本号、 特性、 模块和模块名称的虚拟地址。

下面是输出的从此命令产生的摘录。

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

### <a name="span-idfindmultipleprocessespatternspanspan-idfindmultipleprocessespatternspanfind-multiple-processes-pattern"></a><span id="find_multiple_processes__pattern_"></span><span id="FIND_MULTIPLE_PROCESSES__PATTERN_"></span>找到多个进程 （模式）

以下命令搜索正则表达式，表示进程名称或窗口名称的一个或多个进程的进程。 在此示例中，该命令将为进程搜索其进程名称或窗口名称开头"到"。

```console
c:\>tlist ino*
```

在响应中，TList Inorpc.exe、 Inort.exe，和 Inotask.exe 显示进程详细信息。 有关输出的说明，请参阅"查找进程详细信息使用 PID"子节上面。

### <a name="span-iddisplayaprocesstreetspanspan-iddisplayaprocesstreetspandisplay-a-process-tree-t"></a><span id="display_a_process_tree___t_"></span><span id="DISPLAY_A_PROCESS_TREE___T_"></span>显示进程树 (/ t)

下面的命令显示一个树，它表示在计算机上运行的进程。 进程显示为的创建它们的进程的子级。

```console
c:\>tlist /t
```

生成的进程树遵循。 此树在等显示系统 (4) 进程创建创建 Csrss.exe、 Winlogon.exe、 Lsass.exe 和 Rundll32.exe 的 Smss.exe 进程。 此外，Winlogon.exe 创建 Services.exe，创建了所有与服务相关的进程。

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

### <a name="span-idfindprocessbymodulemspanspan-idfindprocessbymodulemspanfind-process-by-module-m"></a><span id="find_process_by_module___m_"></span><span id="FIND_PROCESS_BY_MODULE___M_"></span>查找进程的模块 (/ m)

以下命令查找所有加载特定 DLL 的进程在计算机上运行。

```console
c:\>tlist /m 
```

在响应中，TList Inorpc.exe、 Inort.exe，和 Inotask.exe 显示进程详细信息。 有关输出的说明，请参阅"查找进程详细信息使用 PID"子节上面。

 

 





