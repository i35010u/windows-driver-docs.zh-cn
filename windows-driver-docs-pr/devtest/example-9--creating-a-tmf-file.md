---
title: 示例9创建 TMF 文件
description: 示例9创建 TMF 文件
ms.assetid: bf66431b-7937-4a98-96cf-e06d28793401
keywords:
- Tracefmt WDK，TMF 文件
- TMF 文件 WDK，Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e6acce66011268d3bd0ddac50ff16014cd0db2f
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769671"
---
# <a name="example-9-creating-a-tmf-file"></a>示例9：创建 TMF 文件


以下命令指示 Tracefmt 在 Tracedrv （Tracedrv 生成的跟踪日志）中格式化和显示跟踪消息。 [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)是设计用于软件跟踪的示例驱动程序，位于 GitHub 上的[Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)存储库中。

该命令包括 **-i**参数，该参数指示 Tracefmt 创建 TRACEDRV 的 TMF 文件。

```
tracefmt d:\tracedrv\tracedrv.etl -i d:\tracedrv\tracedrv.sys -r d:\tracedrv 
-p d:\tracedrv\tmfs -o d:\tracedrv\tracedrv1.txt -v
```

该命令使用 **-i**参数来指示 WDK 中 Tracedrv、Tracedrv 的映像文件的完全限定路径。

```
-i d:\tracedrv\tracedrv.sys
```

它使用 **-r**参数来指示 Tracedrv，TRACEDRV 的 pdb 符号文件的完整版本的完全限定路径。 请注意，使用此参数指定路径，但不指定文件名。 Tracefmt 根据 **-i**指定的图像文件查找符号文件的正确版本。

```
-r d:\tracedrv
```

该命令使用 **-p**参数将 Tracefmt 设置为将它创建的 TMF 文件放在**d： \\ Tracedrv \\ tmfs**目录中。

```
-p d:\tracedrv\tmfs
```

该命令使用 **-o**参数来指示 Tracefmt 将格式化跟踪消息的输出文件放在**d： \\ tracedrv \\ tracedrv1**文件中。 此参数还将摘要文件放在 Tracedrv 文件名称相同的目录中。

```
-o d:\tracedrv\tracedrv1.txt
```

**-V**参数请求详细的（详细）消息。

对于此命令，Tracefmt 在 d： Tracedrv 目录中查找并查找 Tracedrv 的 PDB 文件 \\ 。 它从 PDB 文件中提取跟踪消息格式说明，并将其存储在 TMF 文件中，如下面的输出中的粗体语句中所示。 TMF 文件的名称是 Tracedrv 中跟踪提供程序的[消息 GUID](message-guid.md) 。 Tracefmt 还会创建跟踪消息控制（TMC）文件，并将其放在同一目录中。

Tracefmt 创建 TMF 文件后，它将读取该文件，以便在 Tracedrv 跟踪日志中查找跟踪消息的格式说明。 首先，在 tmf 文件中查找它，并在 d： \\ tracedrv tmfs 目录中查找它创建的 tmf 文件 \\ 。

在对数据进行格式设置之前，Tracefmt 会显示有关跟踪日志的数据。 数据以**Logfile d： \\ tracedrv \\ tracedrv**语句开头。

输出中的最后一条语句显示，Tracefmt 已成功格式化跟踪日志中的13个事件，并创建 Tracedrv1 和 Tracedrv1 文件。

```
Setting log file to: d:\tracedrv\tracedrv.etl

Searching for matching PDB to d:\tracedrv\tracedrv.sys
Current Symbol Search Path = d:\tracedrv

Extracting TMF files out of found PDB files
DBGHELP: d:\tracedrv\tracedrv.pdb - OK
tracefmt : info BNP0000: WPPFMT generating d:\tracedrv\tmfs\1606d1a7-1682-57d1-65f7-36693800e096.tmf for d:\tracedrv\tracedrv.pdb
tracefmt : info BNP0000: WPPFMT generating d:\tracedrv\tmfs\d58c126f-b309-11d1-969e-0000f875a5bc.tmc for d:\tracedrv\tracedrv.pdb
Examining C:\WinDDK\5066\tools\tracing\i386\default.tmf for message formats,  3 found.
Searching for TMF files on path: d:\tracedrv\tmfs
Logfile d:\tracedrv\tracedrv.etl:
        OS version              5.1.2600  (Currently running on 5.1.2600)
        Start Time              2005-06-10-14:25:30.827
        End Time                2005-06-10-14:26:14.371
        Timezone is             Pacific Standard Time (Bias is 480mins)
        BufferSize              8192 B
        Maximum File Size       0 MB
        Buffers  Written        2
        Logger Mode Settings    (0) Logfile Mode is not set
        ProcessorCount          1
06/10/2005-21:25:45.539 ::        1: Filled=     696, Lost=  0 TotalLost= 0

Processing completed   Buffers: 1, Events: 13, EventsLost: 0 :: Format Errors: 0, Unknowns: 0

Event traces dumped to d:\tracedrv\tracedrv1.txt
Event Summary dumped to d:\tracedrv\tracedrv1.txt.sum
```

此 Tracefmt 运行的主输出为 Tracedrv，这是一个文本文件，其中包含 Tracedrv 中的跟踪消息的格式化版本。 以下文本显示 Tracedrv 的内容。

```
EventTrace
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]IOCTL = 1
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 1 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 2 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 3 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Machine State :: Offline
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]IOCTL = 2
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 1 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 2 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 3 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Machine State :: Offline
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
```

 

 





