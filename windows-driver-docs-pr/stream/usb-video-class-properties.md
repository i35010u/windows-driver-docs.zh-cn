---
title: USB 视频类属性
description: USB 视频类的客户端可以使用本主题中所述的以下视频捕获属性集。
ms.assetid: 6295926b-4ec5-42f5-98ca-a375d36f917b
keywords:
- USB 视频类驱动程序 WDK AVStream，属性
- 视频类驱动程序 WDK USB，属性
- UVC 驱动程序 WDK AVStream，属性
- 属性设置 WDK USB 视频类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1454f3a7107afaca69b26289bd3741af00c7024d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383137"
---
# <a name="usb-video-class-properties"></a>USB 视频类属性


USB 视频类的客户端可以使用下面的视频捕获属性集：

[PROPSETID\_VIDCAP\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)
[PROPSETID\_VIDCAP\_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp) USB 视频类的客户端可以发出请求的筛选器或单独的节点。 基于节点的属性的功能等同于 pre USB 视频类基于筛选器的属性。

若要指定基于节点的属性，设置 KSPROPERTY\_类型\_中的标志成员的拓扑标志[ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)结构中的属性描述符包含结构 — 例如， [ **KSPROPERTY\_CAMERACONTROL\_节点\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)。

客户端可以解决多个节点上有单个筛选器，因为 USB 视频类使 Ihv 以支持具有多个独立控制可重用功能区的照相机。

此外，已定义一组新的属性：

[PROPSETID\_VIDCAP\_选择器](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-selector)PROPSETID 中包含的属性项\_VIDCAP\_选择器是基于节点的。

调用[ **KsSynchronousDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)或**DeviceIoControl**以便从用户模式组件的属性请求。 **DeviceIoControl** Microsoft Windows SDK 文档中所述。

在上面的四个属性集包含的属性项的每个 DirectShow COM 接口中有一个相应的方法。 有关方法的详细信息，请参阅 Windows SDK 中的 DirectShow 文档。

USB 视频类设备可以支持某些或所有属性集上面列出。

 

 




