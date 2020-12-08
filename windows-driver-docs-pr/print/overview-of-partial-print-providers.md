---
title: 不完整打印提供程序的概述
description: 不完整打印提供程序的概述
keywords:
- 打印提供程序 WDK，部分打印提供程序
- 网络打印提供程序 WDK，部分打印提供程序
- 部分打印提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 793c5768b0fbd6ad782bb200377c1eb87bb4cca1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807675"
---
# <a name="overview-of-partial-print-providers"></a>不完整打印提供程序的概述





分部提供程序 DLL 通常仅实现管理打印队列和打印作业的提供程序函数的自定义版本。 分部提供程序仅在打印客户端系统上执行，并且依赖于用于驱动程序管理操作的本地打印提供程序以及用于生成打印机数据。 客户端系统上可能存在多个分部提供程序。

在 [打印提供程序定义的函数](functions-defined-by-print-providers.md)中，某些函数标识为 "required"。 部分打印提供程序必须提供所有必需的功能。 部分打印提供程序通常不实现任何可选函数。 所需函数属于以下函数组：

[初始化函数](functions-defined-by-print-providers.md#ddk-initialization-function-gg)

[打印队列管理功能](functions-defined-by-print-providers.md#ddk-print-queue-management-functions-gg)

[打印作业创建函数](functions-defined-by-print-providers.md#ddk-print-job-creation-functions-gg)

[打印作业计划函数](functions-defined-by-print-providers.md#ddk-print-job-scheduling-functions-gg)

[端口管理函数](functions-defined-by-print-providers.md#ddk-port-management-functions-gg)

对于部分打印提供程序，应将打印机端口视为等效于打印队列。 对于接收打印机 \_ 信息 \_ 2 结构 (的任何函数（Microsoft Windows SDK 文档) 中所述），应将结构的 **pPort** 成员设置为打印队列名称。 因此，如果打印队列名称是 \\ \\ 服务器 \\ Printer1，则端口名称也应为 \\ \\ 服务器 \\ Printer1。 部分打印提供程序的 EnumPorts 的实现 (Windows SDK 文档中所述的) 必须返回 Server Printer1 的端口名称 \\ \\ \\ 。

如 [打印提供商简介](introduction-to-print-providers.md)中所述，应用程序对 **OpenPrinter** 的调用会导致后台处理程序的路由器调用每个打印提供程序，直到其中一个用户识别指定的打印队列并返回一个句柄。

请记住，部分打印提供程序不会替换本地提供程序，这一点很重要。 一旦创建了到打印机的用户连接，每次调用提供程序函数时，都会通过本地提供程序进行路由，该提供程序会处理调用本身，或将其路由到部分提供程序。 对标识为 "required" 的访问接口函数的所有调用都将从本地提供程序重新路由到相应的分部提供程序。

分部提供程序不生成打印作业;它们依赖于本地提供程序及其 *打印处理器* 来创建可以发送到打印机的 [原始数据](raw-data-type.md) 。 当打印处理器调用本地提供程序的 **StartDocPrinter** 函数时 (参阅 [打印打印作业](printing-a-print-job.md)) ，而打印队列受分部提供程序支持，则本地提供程序将调用分部提供程序的 **StartDocPrinter** 函数，同时 (文件) 提供原始数据。 分部提供程序的 **StartDocPrinter**、 **WritePrinter** 和 **EndDocPrinter** 函数应通过网络将原始数据发送到远程打印队列。

 

 




