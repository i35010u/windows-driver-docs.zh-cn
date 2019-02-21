---
title: 使用通用安装程序函数
description: 使用通用安装程序函数
ms.assetid: 08a7b585-7930-47a3-9fa0-a36625242e5d
keywords:
- 安装程序 Api 函数 WDK，常规安装函数
- 常规安装函数 WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c38f5cbe6d0158a4362c4a9e35285a2eb28b01f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519236"
---
# <a name="using-general-setup-functions"></a>使用通用安装程序函数





本部分总结了常规的安装程序函数。 *设备安装应用程序*可以使用这些函数来执行以下操作：

-   读取并处理 INF 文件。

-   确定安装的目标系统上的所需的可用空间量。

-   移动文件从安装源介质到介质安装的目标系统上时根据需要请求用户干预。

-   创建一个日志文件在安装过程。

-   将日志项写入[SetupAPI 文本日志](setupapi-text-logs.md)。

安装软件通常使用这些函数一起使用[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)并[PnP 配置管理器函数](https://msdn.microsoft.com/library/windows/hardware/ff549713)。

在本部分中列出的常规安装程序函数中的 Microsoft Windows SDK 文档中详细介绍。

本部分包括以下主题：

[INF 文件处理函数](inf-file-processing-functions.md)

[磁盘提示和错误处理函数](disk-prompting-and-error-handling-functions.md)

[文件队列函数](file-queuing-functions.md)

[默认队列回调例程函数](default-queue-callback-routine-functions.md)

[Cab 文件函数](cabinet-file-function.md)

[磁盘空间列表函数](disk-space-list-functions.md)

[MRU 源列表函数](mru-source-list-functions.md)

[文件的 Log 函数](file-log-functions.md)

[用户界面功能](user-interface-functions.md)

[SetupAPI 日志记录函数](setupapi-logging-functions.md)

 

 





