---
title: 客户端驱动程序堆栈中的 IEC-61883 协议驱动程序
description: 客户端驱动程序堆栈中的 IEC-61883 协议驱动程序
ms.assetid: cee0c0ee-7326-421c-af5a-b483c878b289
keywords:
- IEC-61883 客户端驱动程序 WDK IEEE 1394 总线
- 61883 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf53eb73f74698de2d34f1656bf6630fc1078b9b
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382237"
---
# <a name="iec-61883-protocol-driver-in-a-client-driver-stack"></a>客户端驱动程序堆栈中的 IEC-61883 协议驱动程序





IEC-61883 客户端驱动程序依赖于使用 IEC-61883 协议与设备进行通信的 *61883.sys* 。

下图显示了 AV/C 驱动程序堆栈中 *61883.sys* 的示例。 在此示例中，供应商提供的 AV/C 子单位驱动程序为 IEC-61883 客户端。

![说明 iec-61883 客户端驱动程序堆栈的关系图](images/61883stk.png)

从关系图的顶部开始：

-   Stream 类 driver *stream.sys*支持用于设备（如 DVD、视频捕获和外部声音设备）的内核流式处理驱动程序。 [流式处理微型驱动程序](../stream/streaming-minidrivers2.md)中介绍了 stream 类驱动程序。

-   在此示例中，IEC-61883 客户端是供应商提供的 AV/C 子单位驱动程序。 这是 [编写流微型驱动程序](../stream/writing-a-stream-minidriver.md) ，它使用由 AV/C 堆栈中较低驱动程序提供的设备来控制其设备。  (有关 AV/C 子单位驱动程序的详细信息，请参阅 [av/c 客户端驱动程序](../stream/av-c-client-drivers2.md)。 ) 

    AV/C 子单位驱动程序设置了插件连接和流，并公开了子站点控件、状态和通知。 它们使用内核流式处理框架公开泛型固定属性集和设备特定的属性和事件集。

-   AV/C 流筛选器驱动程序 *avcstrm.sys*是一种可选的 WDM 筛选器驱动程序，用于隔离子单位驱动程序的特定于流的格式处理。 AV/C 流筛选器驱动程序被指定为由第三方 INF 文件更低的驱动程序。 它支持为子单位驱动程序提供 DV 和 MPEG 流格式，并与 *avc.sys*一起提供 CMP helper 函数。 它还提供内核流式处理数据结构和数据交集处理程序。

-   AV/C 协议驱动程序 *avc.sys*将 Av/c 命令映射到 WDM irp，重试请求 (例如，如果某个子单位繁忙) ，则会将临时响应作为挂起的 irp 处理，并根据类型、ID 和操作代码将响应路由到正确的子计划驱动程序。 对于 Microsoft Windows XP 和更高版本， *avc.sys* 还提供了插件连接管理。  (有关 Microsoft 为 AV/C 协议提供的支持的详细信息，请参阅 [av/c 客户端驱动程序](../stream/av-c-client-drivers2.md)。 ) 

-   IEC-61883 协议驱动程序、 *61883.sys*处理函数控制协议 (FCP) 、常见的同步数据包 (CIP) 格式和连接管理过程 (CMP 发送 AV/C 驱动程序堆栈发出的请求。

-   1394总线驱动程序 *1394bus.sys*，枚举 IEEE 1394 总线上的设备，并代表它们响应即插即用和电源管理 irp。

-   主机控制器的端口驱动程序为 IEEE 1394 总线提供与硬件无关的接口。 端口驱动程序处理一些 Irp，并将其他 Irp 转发到主板的主机控制器的端口驱动程序。 Microsoft 提供了标准端口驱动程序， *ohci1394.sys*，适用于满足 *1394 开放主机控制器接口规范*（可从 [IEEE 1394 技术](https://go.microsoft.com/fwlink/p/?linkid=8729) 网站下载）的主机控制器。

AV/C 子单位驱动程序只是一种可能的 IEC-61883 客户端驱动程序类型。 另一个示例是利用在 IEC-61883 之上的 HAVi 协议的驱动程序。 尽管 *61883.sys* 和 IEC-61883 协议没有任何 AV/C 或 HAVi 依赖项，但 *61883.sys* 的客户端可以在不同的约束下运行。 例如，AV/C 子单位驱动程序通常是 *avc.sys*的客户端，它提供与 fcp 相关的功能，并阻止上层驱动程序在堆栈中发送与 fcp 相关的请求，以由 *61883.sys*处理。

 

