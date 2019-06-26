---
title: 客户端驱动程序堆栈中的 IEC-61883 协议驱动程序
description: 客户端驱动程序堆栈中的 IEC-61883 协议驱动程序
ms.assetid: cee0c0ee-7326-421c-af5a-b483c878b289
keywords:
- IEC 61883 客户端驱动程序 WDK IEEE 1394 总线
- 61883 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4375607a13af97ae75a87115a30d7c5604999072
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385785"
---
# <a name="iec-61883-protocol-driver-in-a-client-driver-stack"></a>客户端驱动程序堆栈中的 IEC-61883 协议驱动程序





IEC 61883 客户端驱动程序依赖*是 61883.sys*与他们的设备使用 IEC 61883 协议进行通信。

下图显示的示例*是 61883.sys* AV/C 驱动程序堆栈中。 供应商提供 AV/C 子单元驱动程序是在此示例中的 IEC 61883 客户端。

![说明 iec 61883 客户端驱动程序堆栈的关系图](images/61883stk.png)

从关系图的顶部开始：

-   Stream 类驱动程序， *stream.sys*，支持流式处理 DVD、 视频捕获，以及外部声音设备等设备的驱动程序的内核。 Stream 类驱动程序中记录了[流式处理微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)。

-   在此示例中，IEC 61883 客户端是一个供应商提供 AV/C 子单元驱动程序。 这是[编写 Stream 微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/writing-a-stream-minidriver)使用 AV/C 堆栈中的低级驱动程序提供的功能来控制其设备。 (有关 AV/C 子单元驱动程序的详细信息，请参阅[AV/C 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-client-drivers2)。)

    AV/C 子单元驱动程序设置插入连接和流，并公开子单元控件、 状态和通知。 它们使用流式处理 framework 内核来公开泛型 pin 属性集以及特定于设备的属性和事件集。

-   AV/C 流筛选器驱动程序， *avcstrm.sys*，是可选的 WDM 筛选器驱动程序，将子单元驱动程序的特定于流的格式处理中隔离出来。 AV/C 流筛选器驱动程序指定为一个较低的驱动程序通过第三方 INF 文件。 它的子单元驱动程序支持 DV 和 MPEG 流格式，并提供了与结合 CMP 帮助器函数*avc.sys*。 它还提供内核流式处理数据结构和数据交集处理程序。

-   AV/C 协议驱动程序， *avc.sys*，映射到 WDM Irp AV/C 的命令，重试次数 （例如，如果子单元正在使用中），请求处理临时响应作为挂起的 Irp 和路由响应到正确的子单元驱动程序根据类型、 ID、和操作代码。 Microsoft Windows XP 及更高版本， *avc.sys*还提供即插即用连接管理。 (有关 Microsoft 提供的用于 AV/C 协议的支持的详细信息，请参阅[AV/C 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-client-drivers2)。)

-   IEC 61883 协议驱动程序，*是 61883.sys*，处理函数控制协议 (FCP)、 常见的同步数据包 (CIP) 格式，以及连接管理过程 (CMP) 下 AV/C 驱动程序堆栈发送的请求。

-   1394 总线驱动程序， *1394bus.sys*、 枚举 IEEE 1394 总线上的设备，并对插和代表这些设备上的电源管理 Irp 的响应。

-   主控制器端口驱动程序提供了 IEEE 1394 总线的独立于硬件的界面。 端口驱动程序处理某些 Irp，并将其他人转发给主板的主控制器端口驱动程序。 Microsoft 提供的标准端口驱动程序中， *ohci1394.sys*，为满足主机控制器*1394年打开主机控制器接口规范*，这是可从下载[IEEE 1394 技术](https://go.microsoft.com/fwlink/p/?linkid=8729)网站。

AV/C 子单元驱动程序是只是其中之一的 IEC 61883 客户端驱动程序的可能类型。 另一个示例是使用 HAVi 协议上 IEC 61883 分层的驱动程序。 尽管*是 61883.sys*和 IEC 61883 协议不具有任何 AV/C 或 HAVi 依赖项的客户端*是 61883.sys*可以在不同的约束下操作。 例如，AV/C 子单元驱动程序通常是客户端*avc.sys*，其中提供了与 FCP 相关的函数和发送与 FCP 相关的请求的块别的驱动程序向下堆栈来处理*是 61883.sys*.

 

 




