---
title: PROPSETID\_VIDCAP\_扩展\_单元
description: PROPSETID\_VIDCAP\_扩展\_单元
ms.assetid: 7aa4742f-e64f-4798-a9e0-8c1f02aa15b3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea91bcafc546844181194ab2534128a45f087eb2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845305"
---
# <a name="propsetid_vidcap_extension_unit"></a>PROPSETID\_VIDCAP\_扩展\_单元


## <span id="ddk_propsetid_vidcap_extension_unit_ks"></span><span id="DDK_PROPSETID_VIDCAP_EXTENSION_UNIT_KS"></span>


PROPSETID\_VIDCAP\_扩展\_单元属性集是与[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)一起使用的新的。

对于实现供应商特定扩展单元的设备，支持此属性集。 供应商提供的属性页和应用程序通过通用[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol) COM 接口访问此属性集。

*Ksmedia*中的 KSPROPERTY\_扩展\_单元枚举指定此集的属性。

对此属性集的支持是可选的，只应由提供供应商定义的硬件控制的设备来实现。

USB 视频类驱动程序的客户端可以发出以下筛选器或节点请求：

[**KSPROPERTY\_扩展\_单元\_信息**](ksproperty-extension-unit-info.md)

### <a name="span-iddirectshow_interfacesspanspan-iddirectshow_interfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow 接口

使用以下用户模式接口访问此集的属性： **IKsTopologyInfo**、 **ISelector**和**IKsNodeControl**。 有关这些接口的信息，请参阅 Microsoft Windows SDK 中的 DirectShow 文档。

 

 





