---
title: 本地打印提供程序
description: 本地打印提供程序
ms.assetid: c6f9ba42-5f0f-4919-bfac-e4cd1045de4d
keywords:
- 打印提供程序 WDK，本地打印提供商
- 本地打印提供商 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70124be0c3ae0e867c4447231b959a288917bd1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388088"
---
# <a name="local-print-provider"></a>本地打印提供程序





**警告**  从 Windows 10 开始，支持第三方打印提供商的 Api 已弃用。 Microsoft 不建议到第三方打印提供商的任何投资。 此外，在 Windows 8 和更高版本的 v4 打印驱动程序模型是可用的产品，第三方打印提供商不可能创建，或管理使用 v4 打印驱动程序的队列。

 

在本地打印提供程序适用于 Microsoft Windows 2000 和更高版本提供了作业控制和打印机管理功能通过本地访问的所有打印机的打印提供程序的端口监视器。 (客户端管理员通过选择来设置对此类打印机的访问**本地打印机**选项使用添加打印机向导时。)此类打印机包括连接到本地系统的串行和并行端口。 它们还可以包括与其他的 I/O 通道，如 SCSI 端口，以及连接到非-NT-基于-操作系统的远程系统服务器的打印机连接的设备。

本地打印提供程序实现的整套[函数定义的打印提供商](functions-defined-by-print-providers.md)。 它还会提供以下功能：

-   打印作业后台处理程序，使用 despooling 定向到从本地访问的作业的打印队列。

-   对 Windows 2000 和更高版本的操作系统版本的支持[打印机驱动程序体系结构](printer-driver-architecture.md)调用本地打印机接口的 Dll。

-   对供应商提供的打印处理器的支持 (请参阅[编写打印处理器](writing-a-print-processor.md))。

-   供应商提供的打印监视器支持 (请参阅[编写打印监视器](writing-a-print-monitor.md))。

当应用程序创建打印作业时下, 图将提供在本地打印机之间的控制流 （某种程度上简化） 视图提供程序的组件。

![当应用程序创建打印作业说明在本地打印机提供程序的组件之间的控制流的视图的关系图](images/contflow.png)

如图所示，应用程序通过调用图形驱动程序接口 (GDI) 创建打印作业。 无论是否打印作业的最初的输出格式都是 EMF，本地打印提供程序的作业创建 API 创建一个假脱机文件。 更高版本，该作业计划时，假脱机文件为只读并且如果格式*增强型图元文件 (EMF)*，EMF 打印处理器将作业发送回转换为原始格式，借助 GDI[打印机图形 DLL](printer-graphics-dll.md). 已转换的数据流可以然后发送回通过本地打印提供程序到打印机 （不带正在后台）。

可以创建一个供应商*部分的打印提供商*，可结合使用本地的打印提供商，以支持自定义网络配置。

 

 




