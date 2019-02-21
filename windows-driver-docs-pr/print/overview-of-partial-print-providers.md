---
title: 部分打印提供商的概述
description: 部分打印提供商的概述
ms.assetid: 622f99e3-d4a5-42f0-ab71-4d256e0ea02c
keywords:
- 打印提供程序 WDK，部分打印提供商
- 网络打印提供商 WDK，部分打印提供商
- 部分的打印提供商 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4115664165373c56a771180dad0187f65636830
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555099"
---
# <a name="overview-of-partial-print-providers"></a>部分打印提供商的概述





部分提供程序 DLL 通常实现仅用于管理打印队列和打印作业的提供程序函数的自定义的版本。 部分提供程序只能在打印客户端系统上执行，并取决于本地打印提供程序的驱动程序管理操作和用于生成打印机的数据。 客户端系统上可以存在多个部分的提供程序。

在中[打印提供商定义的函数](functions-defined-by-print-providers.md)，某些函数标识为"必需"。 部分打印提供商必须提供所需的所有函数。 部分打印提供商通常不会实现任何可选函数。 下面的函数组的成员所需的功能：

[初始化函数](functions-defined-by-print-providers.md#ddk-initialization-function-gg)

[打印队列管理功能](functions-defined-by-print-providers.md#ddk-print-queue-management-functions-gg)

[打印作业创建函数](functions-defined-by-print-providers.md#ddk-print-job-creation-functions-gg)

[打印作业计划功能](functions-defined-by-print-providers.md#ddk-print-job-scheduling-functions-gg)

[端口的管理功能](functions-defined-by-print-providers.md#ddk-port-management-functions-gg)

对于部分打印提供程序，应考虑的打印机端口为相当于打印队列。 接收打印机的任何函数\_INFO\_（Microsoft Windows SDK 文档中所述） 的 2 个结构，该结构的**pPort**成员应设置为打印队列名称。 因此如果打印队列名称为\\\\服务器\\Printer1，还应为端口名称\\ \\Server\\Printer1。 EnumPorts （Windows SDK 文档中所述） 部分的打印提供程序实现必须返回的端口名\\ \\Server\\Printer1。

如中所述[打印提供程序简介](introduction-to-print-providers.md)，应用程序的调用**OpenPrinter**导致后台处理程序的路由器，用于调用每个打印提供程序，直到其中一个识别指定的打印队列并返回一个句柄。

请务必记住部分的打印提供程序不会替换本地提供程序。 一旦创建到打印机的用户连接后，每次调用提供程序函数通过本地提供程序，后者处理调用本身或网络部分的提供程序到路由。 对标识为"required"进行的提供程序函数的所有调用会从本地访问接口重新都路由到相应的部分提供程序。

部分提供程序不会生成打印作业;它们依赖于本地的提供程序并将其*打印处理器*来创建[原始数据](raw-data-type.md)，可以发送到打印机。 当打印处理器调用本地提供程序**StartDocPrinter**函数 (请参阅[打印打印作业](printing-a-print-job.md))，并且部分的访问接口支持打印队列，而本地提供程序调用分部提供商**StartDocPrinter**函数，提供原始数据 （作为文件）。 部分提供商**StartDocPrinter**， **WritePrinter**，并**EndDocPrinter**函数应原始数据通过网络发送到远程打印队列。

 

 




