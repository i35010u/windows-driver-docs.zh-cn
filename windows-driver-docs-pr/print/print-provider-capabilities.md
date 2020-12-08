---
title: 打印提供程序的功能
description: 打印提供程序的功能
keywords:
- 打印提供商 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce55330927c9be05ed379e8031f0f973497fcdfe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807461"
---
# <a name="print-provider-capabilities"></a>打印提供程序的功能





**警告**  
从 Windows 10 开始，不推荐使用支持第三方打印提供程序的 Api。 Microsoft 不建议对第三方打印提供商进行任何投资。 此外，在可用 v4 打印驱动程序模型的 Windows 8 和更高版本产品上，第三方打印提供商可能不会创建或管理使用 v4 打印驱动程序的队列。

 

通过支持预定义的 API 函数集，Microsoft Windows 2000 和更高版本的打印提供程序可提供以下功能：

-   打印队列管理

    添加、删除、打开、关闭、枚举和设置打印队列的参数。 此外，还提供了对打印队列状态更改的通知。

-   打印机驱动程序管理

    添加、删除、枚举和指定打印机驱动程序的目录。

-   打印作业创建

    开始和结束文档，开始和结束文档页，将作业的数据流写入端口，读取打印机状态信息。

-   打印作业计划

    为打印作业计划、枚举和设置参数。

-   表单管理

    添加、删除、枚举和设置打印窗体的参数。

-   打印处理器管理

    添加、删除、枚举、指定的目录以及打印处理器支持的数据类型。

-   打印监视器管理

    添加、删除和枚举打印监视器。

-   端口管理

    添加、删除、配置、枚举和设置打印机端口的参数。

-   注册表管理

    创建、删除和枚举与打印提供程序相关联的注册表项和值。

-   其他功能

    显示一个消息框，关闭打印提供程序，读取内存映射的假脱机文件，提供端口监视器 UI Dll 和端口监视器服务器 Dll 之间的通信路径。

这些功能以一组 [由打印提供程序定义的函数](functions-defined-by-print-providers.md)来实现。

 

 




