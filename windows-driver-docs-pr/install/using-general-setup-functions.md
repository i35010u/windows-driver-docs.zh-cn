---
title: 使用常规设置函数
description: 使用常规设置函数
keywords:
- Setupapi.log 函数 WDK，常规设置功能
- 常规设置函数 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 912f173e9707b1108cacb4e35085dff4e360437b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827035"
---
# <a name="using-general-setup-functions"></a>使用常规设置函数





本部分总结了一般的设置功能。 *设备安装应用程序* 可以使用这些功能来执行以下操作：

-   读取和处理 INF 文件。

-   确定安装的目标系统上所需的可用空间量。

-   将文件从安装源媒体移到安装的目标系统上的媒体，同时根据需要请求用户干预。

-   创建在安装期间移动的文件日志。

-   将日志条目写入 [setupapi.log 文本日志](setupapi-text-logs.md)。

安装软件通常使用这些功能以及 [设备安装功能](/previous-versions/ff541299(v=vs.85)) 和 [PnP 配置管理器功能](/previous-versions/ff549713(v=vs.85))。

Microsoft Windows SDK 文档中详细介绍了本节中列出的常规设置函数。

本节包括下列主题：

[INF 文件处理函数](inf-file-processing-functions.md)

[磁盘提示和错误处理函数](disk-prompting-and-error-handling-functions.md)

[文件排队函数](file-queuing-functions.md)

[默认的队列回调常规函数](default-queue-callback-routine-functions.md)

[Cabinet 文件函数](cabinet-file-function.md)

[磁盘空间列表函数](disk-space-list-functions.md)

[MRU 源列表函数](mru-source-list-functions.md)

[文件日志函数](file-log-functions.md)

[用户界面函数](user-interface-functions.md)

[SetupAPI 日志记录函数](setupapi-logging-functions.md)

 

