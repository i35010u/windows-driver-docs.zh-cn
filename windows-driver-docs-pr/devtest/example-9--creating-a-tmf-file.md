---
title: 示例 9 创建 TMF 文件
description: 示例 9 创建 TMF 文件
ms.assetid: bf66431b-7937-4a98-96cf-e06d28793401
keywords:
- Tracefmt WDK，TMF 文件
- TMF 文件 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a4a49d75f47d4f1a194952d376f357e2227a0b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547378"
---
# <a name="example-9-creating-a-tmf-file"></a>示例 9:创建 TMF 文件


以下命令将定向 Tracefmt 来格式化和 Tracedrv.etl，由 Tracedrv 生成跟踪日志中显示跟踪消息。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)，为软件跟踪设计的一个示例驱动程序现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

该命令包含 **-i**参数，它指示 Tracefmt 为 Tracedrv 创建 TMF 文件。

```
tracefmt d:\tracedrv\tracedrv.etl -i d:\tracedrv\tracedrv.sys -r d:\tracedrv 
-p d:\tracedrv\tmfs -o d:\tracedrv\tracedrv1.txt -v
```

该命令使用 **-i**参数来为 Tracedrv，Tracedrv.sys，WDK 中指示的图像文件的完全限定的路径。

```
-i d:\tracedrv\tracedrv.sys
```

它使用 **-r**参数为 Tracedrv，Tracedrv.pdb 指明的 PDB 符号文件的完整版本的完全限定的路径。 请注意，此参数，但不是文件的名称与指定的路径。 Tracefmt 查找符号文件基于指定的图像文件的正确版本 **-i**。

```
-r d:\tracedrv
```

该命令使用 **-p**参数指示 Tracefmt 将它为 Tracedrv 中创建该 TMF 文件放**d:\\tracedrv\\tmfs**目录。

```
-p d:\tracedrv\tmfs
```

该命令使用 **-o**参数指示 Tracefmt 放置的输出文件格式中的跟踪消息**d:\\tracedrv\\tracedrv1.txt**文件。 此参数还会摘要文件放置在同一个目录并使用 Tracedrv.txt.sum 文件名称。

```
-o d:\tracedrv\tracedrv1.txt
```

**-V**参数请求 （详细） 的详细的消息。

此命令的响应，Tracefmt 查找，并查找 PDB 文件在 d: Tracedrv.sys\\tracedrv 目录。 它提取跟踪消息格式的 PDB 文件中的说明，并将其存储在 TMF 文件中，在语句中以粗体类型遵循在输出中所示。 TMF 文件的名称是[消息 GUID](message-guid.md) Tracedrv 的跟踪提供程序。 Tracefmt 还创建一个跟踪消息控件 (TMC) 文件，并将其放在同一目录中。

Tracefmt 创建 TMF 文件后，它会读取要查找的跟踪消息的格式设置说明 Tracedrv.etl 跟踪日志中的文件。 它首先查找 TMf 文件中的 d： 创建其 Default.tmf 文件中查找\\tracedrv\\tmfs 目录。

它设置数据的格式之前，Tracefmt 显示有关跟踪日志的数据。 数据开头**日志文件 d:\\tracedrv\\tracedrv.etl**语句。

在输出中的最后一个语句显示 Tracefmt 成功格式的跟踪日志中的 13 事件和创建的 Tracedrv1.txt 和 Tracedrv1.txt.sum 文件。

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

此 Tracefmt 运行的主输出是 Tracedrv.txt，包含 Tracedrv.etl 中的跟踪消息的格式化的版本的文本文件。 以下文本显示了 Tracedrv.txt 的内容。

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

 

 





