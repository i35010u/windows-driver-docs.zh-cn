---
title: PROPSETID\_VIDCAP\_EXTENSION\_UNIT
description: PROPSETID\_VIDCAP\_EXTENSION\_UNIT
ms.assetid: 7aa4742f-e64f-4798-a9e0-8c1f02aa15b3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5471b3d12202abc7dfd54635392309833c6e532
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379058"
---
# <a name="propsetidvidcapextensionunit"></a>PROPSETID\_VIDCAP\_EXTENSION\_UNIT


## <span id="ddk_propsetid_vidcap_extension_unit_ks"></span><span id="DDK_PROPSETID_VIDCAP_EXTENSION_UNIT_KS"></span>


PROPSETID\_VIDCAP\_扩展\_单元属性集是用于新[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)。

实现特定于供应商扩展单元的设备支持设置此属性。 供应商提供的属性页和应用程序访问此属性设置通过通用[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol) COM 接口。

KSPROPERTY\_扩展\_中的单元枚举*ksmedia.h*指定此集的属性。

支持设置此属性是可选的应仅由设备提供供应商定义的硬件控件的实现。

USB 视频类驱动程序的客户端可以发出以下请求的筛选器或节点：

[**KSPROPERTY\_EXTENSION\_UNIT\_INFO**](ksproperty-extension-unit-info.md)

### <a name="span-iddirectshowinterfacesspanspan-iddirectshowinterfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow 接口

使用以下用户模式接口来访问此集的属性：**IKsTopologyInfo**， **ISelector**，和**IKsNodeControl**。 请参阅适用于这些接口的信息的 Microsoft Windows SDK 中的 DirectShow 文档。

 

 





