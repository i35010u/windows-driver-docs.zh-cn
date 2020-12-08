---
title: 示例7自定义跟踪消息前缀
description: 示例7自定义跟踪消息前缀
keywords:
- Tracefmt WDK，前缀
- Tracefmt 的前缀
- 跟踪消息前缀 WDK Tracefmt
- 自定义跟踪消息前缀 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28cca8e97be475c949718e75ad717c940ed96d50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804281"
---
# <a name="example-7-customizing-the-trace-message-prefix"></a>示例 7：自定义跟踪消息前缀


每个跟踪消息都以 [跟踪消息前缀](trace-message-prefix.md) 开始，其中包含跟踪消息的相关数据。 跟踪消息前缀的格式存储在% TRACE \_ format \_ prefix% 环境变量中。 通过更改环境变量的值，可以自定义跟踪消息前缀，以使用最有用的格式来显示跟踪消息所需的数据。 默认跟踪消息前缀中的变量以及可以在跟踪消息前缀中使用的所有变量都在跟踪消息前缀主题中进行了介绍。

下面的显示显示默认跟踪消息前缀。 跟踪消息是由 Tracedrv 生成的，Windows 驱动程序工具包中的启用跟踪的示例驱动程序)  (WDK。

```
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]IOCTL = 1
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]Hello, 1 Hi
[0]0AF4.0C64::07/25/2003-14:55:39.998 [tracedrv]Hello, 2 Hi
...
```

默认前缀的格式如下所示。

```
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

表示以下数据的：

```
[CPUNumber]ProcessID.ThreadID::SystemTime [MessageGUIDFriendlyName]
```

其中， *MessageGUIDFriendlyName* 是在默认情况下，在其中生成跟踪提供程序的目录的名称。

若要创建新的跟踪消息前缀，请使用 **set** 命令重置% trace \_ FORMAT \_ prefix% 环境变量的值。 例如，

```
set TRACE_FORMAT_PREFIX=%2!s!: %!FUNC!: %8!04x!.%3!04x!: %4!s!:
```

此命令设置以下格式的跟踪消息前缀：

```
SourceFile_LineNumber: FunctionName: ProcessID.ThreadID: SystemTime 
```

因此，Tracefmt 输出将使用新的跟踪消息前缀，如以下显示所示：

```
tracedrv_c258: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  IOCTL = 1
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 1 Hi
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 2 Hi
tracedrv_c264: TracedrvDispatchDeviceControl: 0af4.0c64: 07/25/2003-13:55:39.998:  Hello, 3 Hi
```

...

**注意**   如果要在命令或批处理文件中设置跟踪前缀，其中 percent 符号表示命令行参数的变量，请使用两个连续百分比符号作为前缀变量。 例如，若要在前缀中包括系统时间，请键入 **% %4**。

 

 

 





