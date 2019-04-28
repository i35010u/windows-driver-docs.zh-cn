---
title: 示例 7 自定义跟踪消息前缀
description: 示例 7 自定义跟踪消息前缀
ms.assetid: 75beccef-fd0b-4a4f-9ea2-11940b5baddf
keywords:
- Tracefmt WDK 前缀
- 前缀 WDK Tracefmt
- 跟踪消息前缀 WDK Tracefmt
- 自定义跟踪消息前缀 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45ef8258a2b8252951b6fd602a080af8d5cb7bb9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352897"
---
# <a name="example-7-customizing-the-trace-message-prefix"></a>示例 7：自定义跟踪消息前缀


每条跟踪消息开头[跟踪消息前缀](trace-message-prefix.md)组成有关跟踪消息的数据。 跟踪消息前缀的格式存储在 %跟踪\_格式\_前缀 %环境变量。 通过更改环境变量的值，可以自定义要显示有关中对您最有用的格式的跟踪消息所需的数据的跟踪消息前缀。 中默认跟踪消息前缀的变量和可以使用跟踪消息前缀中的所有变量都跟踪消息前缀主题中所述。

以下屏幕将显示默认跟踪消息前缀。 跟踪消息生成的 Tracedrv，启用跟踪的示例驱动程序 Windows Driver Kit (WDK) 中。

```
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]IOCTL = 1
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]Hello, 1 Hi
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]Hello, 2 Hi
...
```

默认的前缀的格式如下所示。

```
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

表示以下数据：

```
[CPUNumber]ProcessID.ThreadID::SystemTime [MessageGUIDFriendlyName]
```

其中*MessageGUIDFriendlyName*是目录的名称，默认情况下，在生成的跟踪提供程序。

若要创建新的跟踪消息前缀，使用**设置**命令来重置 %跟踪的值\_格式\_前缀 %环境变量。 例如，

```
set TRACE_FORMAT_PREFIX=%2!s!: %!FUNC!: %8!04x!.%3!04x!: %4!s!:
```

此命令设置格式的跟踪消息前缀：

```
SourceFile_LineNumber: FunctionName: ProcessID.ThreadID: SystemTime 
```

因此，Tracefmt 输出会使用新的跟踪消息前缀，显示在下面所示：

```
tracedrv_c258: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  IOCTL = 1
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 1 Hi
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 2 Hi
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 3 Hi
```

...

**请注意**  如果您在设置跟踪前缀中的命令或批处理文件，其中百分比符号表示命令行参数的变量，使用两个连续的百分比符号为前缀的变量。 例如，若要包含的前缀中的系统时间，请键入 **%%**。

 

 

 





