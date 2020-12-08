---
title: USB 视频类属性
description: USB 视频类的客户端可以使用本主题中所述的以下视频捕获属性集。
keywords:
- USB 视频类驱动程序 WDK AVStream，属性
- 视频类驱动程序 WDK USB，属性
- UVC 驱动程序 WDK AVStream，属性
- 属性集 WDK USB 视频类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91ee5b8b9623a99b6b2ce1faf6dc949f913afd7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795257"
---
# <a name="usb-video-class-properties"></a>USB 视频类属性


USB 视频类的客户端可以使用以下视频捕获属性集：

[PROPSETID \_VIDCAP \_ CAMERACONTROL](./propsetid-vidcap-cameracontrol.md) 
 [PROPSETID \_ VIDCAP \_ VIDEOPROCAMP](./propsetid-vidcap-videoprocamp.md)客户端 USB 视频类可对筛选器或单个节点发出请求。 基于节点的属性的功能与基于 USB 视频类筛选器的属性的功能相同。

若要指定基于节点的属性，请 \_ \_ 在属性描述符结构中包含的 [**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) 结构的 FLAGS 成员中设置 KSPROPERTY 类型拓扑标志，例如 [**KSPROPERTY \_ CAMERACONTROL \_ node \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)。

由于客户端可以在单个筛选器上处理多个节点，因此 USB Video 类使 Ihv 能够支持具有多个独立控制重用功能区的相机。

此外，还定义了一个新的属性集：

[PROPSETID \_VIDCAP \_ 选择器](./propsetid-vidcap-selector.md) PROPSETID VIDCAP 选择器中包含的属性项 \_ \_ 基于节点。

调用 [**KsSynchronousDeviceControl**](/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol) 或 **DeviceIoControl** ，以发出来自用户模式组件的属性请求。 Microsoft Windows SDK 文档中介绍了 **DeviceIoControl** 。

以上四个属性集中包含的每个属性项在 DirectShow COM 接口中都有相应的方法。 有关这些方法的详细信息，请参阅 Windows SDK 中的 DirectShow 文档。

USB 视频类设备可以支持上面列出的部分或全部属性集。

 

