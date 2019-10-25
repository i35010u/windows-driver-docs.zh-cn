---
title: USB 视频类属性
description: USB 视频类的客户端可以使用本主题中所述的以下视频捕获属性集。
ms.assetid: 6295926b-4ec5-42f5-98ca-a375d36f917b
keywords:
- USB 视频类驱动程序 WDK AVStream，属性
- 视频类驱动程序 WDK USB，属性
- UVC 驱动程序 WDK AVStream，属性
- 属性集 WDK USB 视频类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dae84f8a8162d842e71e30d835353dcb6ad1ede
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844656"
---
# <a name="usb-video-class-properties"></a>USB 视频类属性


USB 视频类的客户端可以使用以下视频捕获属性集：

[PROPSETID\_VIDCAP\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)
[PROPSETID\_VIDCAP\_](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp) USB 视频类的 VIDEOPROCAMP 客户端可以对筛选器或单个节点发出请求。 基于节点的属性的功能与基于 USB 视频类筛选器的属性的功能相同。

若要指定基于节点的属性，请设置属性描述符结构中包含的[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)结构的 Flags 成员中的 KSPROPERTY\_类型\_拓扑标志，例如[**KSPROPERTY\_CAMERACONTROL\_节点\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)。

由于客户端可以在单个筛选器上处理多个节点，因此 USB Video 类使 Ihv 能够支持具有多个独立控制重用功能区的相机。

此外，还定义了一个新的属性集：

[PROPSETID\_VIDCAP\_选择器](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-selector)PROPSETID\_VIDCAP\_选择器中包含的属性项基于节点。

调用[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)或**DeviceIoControl** ，以发出来自用户模式组件的属性请求。 Microsoft Windows SDK 文档中介绍了**DeviceIoControl** 。

以上四个属性集中包含的每个属性项在 DirectShow COM 接口中都有相应的方法。 有关这些方法的详细信息，请参阅 Windows SDK 中的 DirectShow 文档。

USB 视频类设备可以支持上面列出的部分或全部属性集。

 

 




