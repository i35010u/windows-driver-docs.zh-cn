---
title: 打印提供程序的功能
description: 打印提供程序的功能
ms.assetid: 1b01aac5-673a-4593-a52e-6017d9683c42
keywords:
- 打印提供程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fede6441e8c1268b00815b68219ad9fca52305c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377875"
---
# <a name="print-provider-capabilities"></a>打印提供程序的功能





**警告**  从 Windows 10 开始，支持第三方打印提供商的 Api 已弃用。 Microsoft 不建议到第三方打印提供商的任何投资。 此外，在 Windows 8 和更高版本的 v4 打印驱动程序模型是可用的产品，第三方打印提供商不可能创建，或管理使用 v4 打印驱动程序的队列。

 

通过支持预定义的 API 集函数、 Microsoft Windows 2000 和更高版本的打印提供商可以提供以下功能：

-   打印队列管理

    添加、 删除、 打开、 关闭、 枚举，以及设置打印队列的参数。 此外，提供打印队列的状态更改的通知。

-   打印机驱动程序管理

    添加、 删除、 枚举和指定的打印机驱动程序的目录。

-   创建打印作业

    起始和结束一个文档，起始和结束文档页上，写入到的端口，读取打印机状态信息的作业的数据流。

-   打印作业计划

    计划、 枚举和设置打印作业的参数。

-   窗体管理

    添加、 删除、 枚举，以及设置打印窗体的参数。

-   打印处理器管理

    添加、 删除、 枚举、 指定的目录和打印处理器支持的数据类型。

-   打印监视器管理

    添加、 删除和枚举打印监视器。

-   端口管理

    添加、 删除、 配置、 枚举和设置参数的打印机端口。

-   注册表管理

    创建、 删除和枚举注册表项和与打印提供程序关联的值。

-   其他功能

    显示一个消息框，关闭打印提供程序，读取内存映射假脱机文件，提供端口监视器用户界面的 Dll 和端口监视服务器 Dll 之间的通信路径。

这些功能实现为一系列[函数定义的打印提供商](functions-defined-by-print-providers.md)。

 

 




