---
title: 本地打印提供程序
description: 本地打印提供程序
keywords:
- 打印提供程序 WDK，本地打印提供程序
- 本地打印提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e490216d04893475025ea931399a8ddfbf019a0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807935"
---
# <a name="local-print-provider"></a>本地打印提供程序





**警告**  
从 Windows 10 开始，不推荐使用支持第三方打印提供程序的 Api。 Microsoft 不建议对第三方打印提供商进行任何投资。 此外，在可用 v4 打印驱动程序模型的 Windows 8 和更高版本产品上，第三方打印提供商可能不会创建或管理使用 v4 打印驱动程序的队列。

 

Microsoft Windows 2000 和更高版本的本地打印提供程序为通过本地打印提供程序的端口监视器访问的所有打印机提供作业控制和打印机管理功能。  (客户端管理员通过在使用 "添加打印机向导" 时选择 " **本地打印机** " 选项来设置对此类打印机的访问。 ) 此类打印机包括那些连接到本地系统的串行端口和并行端口的打印机。 它们还可以包括连接到其他 i/o 通道（如 SCSI 端口）的设备，以及连接到远程非基于 NT 的操作系统服务器的打印机。

本地打印提供程序实现了 [由打印提供程序定义](functions-defined-by-print-providers.md)的整个函数集。 它还提供以下功能：

-   打印作业后台处理程序，其中包含定向到本地可访问打印队列的作业 despooling。

-   支持 Windows 2000 及更高版本的操作系统版本 [打印机驱动程序体系结构](printer-driver-architecture.md) ，同时调用本地打印机接口 dll。

-   支持供应商提供的打印处理器 (参阅 [写入打印处理器](writing-a-print-processor.md)) 。

-   支持供应商提供的打印监视器 (参阅 [写入打印监视器](writing-a-print-monitor.md)) 。

下图提供了一个 (在应用程序创建打印作业时，在本地打印机提供商的组件中部分简化的控制流) 视图。

![说明在应用程序创建打印作业时本地打印机提供程序组件之间的控制流视图的关系图](images/contflow.png)

如图所示，应用程序通过调用图形驱动程序接口 (GDI) 来创建打印作业。 无论打印作业的初始输出格式是否为 EMF，本地打印提供程序的作业创建 API 都将创建一个假脱机文件。 稍后，当计划作业时，将读取假脱机文件，如果格式为 *增强型图元文件 (EMF)*，EMF 打印处理器会将该作业发送回 GDI，以转换为 RAW 格式，同时提供 [打印机图形 DLL](printer-graphics-dll.md)的帮助。 然后，转换后的数据流可以通过本地打印提供程序发回给打印机 (，而不会 respooled) 。

供应商可以创建 *部分打印提供* 程序，这些提供程序与本地打印提供程序协同工作以支持自定义网络配置。

 

 




