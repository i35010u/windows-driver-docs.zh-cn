---
title: PROPSETID \_ VIDCAP \_ 扩展 \_ 单元
description: PROPSETID \_ VIDCAP \_ 扩展 \_ 单元
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f6ed9a1cf502ad4ff04550980b9728477c2b43d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824407"
---
# <a name="propsetid_vidcap_extension_unit"></a>PROPSETID \_ VIDCAP \_ 扩展 \_ 单元


## <span id="ddk_propsetid_vidcap_extension_unit_ks"></span><span id="DDK_PROPSETID_VIDCAP_EXTENSION_UNIT_KS"></span>


PROPSETID \_ VIDCAP \_ EXTENSION \_ UNIT 属性集是与 [USB 视频类驱动程序](./usb-video-class-driver.md)一起使用的新设置。

对于实现供应商特定扩展单元的设备，支持此属性集。 供应商提供的属性页和应用程序通过通用 [IKsControl](/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol) COM 接口访问此属性集。

\_Ksmedia 中的 KSPROPERTY 扩展 \_ 单元 *ksmedia.h* 枚举指定此集的属性。

对此属性集的支持是可选的，只应由提供供应商定义的硬件控制的设备来实现。

USB 视频类驱动程序的客户端可以发出以下筛选器或节点请求：

[**KSPROPERTY \_ 扩展 \_ 单元 \_ 信息**](ksproperty-extension-unit-info.md)

### <a name="span-iddirectshow_interfacesspanspan-iddirectshow_interfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow 接口

使用以下用户模式接口访问此集的属性： **IKsTopologyInfo**、 **ISelector** 和 **IKsNodeControl**。 有关这些接口的信息，请参阅 Microsoft Windows SDK 中的 DirectShow 文档。

 

