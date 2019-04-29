---
title: PROPSETID\_EXT\_DEVICE
description: PROPSETID\_EXT\_DEVICE
ms.assetid: fe1a14dc-b337-462b-ac2a-10eef036ef7f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cd96de0d8bd0eb7a34fa9a8e087e6005cf4182e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362193"
---
# <a name="propsetidextdevice"></a>PROPSETID\_EXT\_DEVICE


## <span id="ddk_propsetid_ext_device_ks"></span><span id="DDK_PROPSETID_EXT_DEVICE_KS"></span>


PROPSETID\_EXT\_设备属性设置控件微型 DV 摄像机等外部设备。

KSPROPERTY\_中的 EXTDEVICE 枚举*ksmedia.h*指定此集的属性。

对设置此属性是可选的仅支持外部视频捕获设备的微型驱动程序应实现的支持。

[**KSPROPERTY\_EXTDEVICE\_ID**](ksproperty-extdevice-id.md)

[**KSPROPERTY\_EXTDEVICE\_VERSION**](ksproperty-extdevice-version.md)

[**KSPROPERTY\_EXTDEVICE\_POWER\_STATE**](ksproperty-extdevice-power-state.md)

[**KSPROPERTY\_EXTDEVICE\_PORT**](ksproperty-extdevice-port.md)

[**KSPROPERTY\_EXTDEVICE\_CAPABILITIES**](ksproperty-extdevice-capabilities.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMExtDevice**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档） 提供对此集的属性的访问。

 

 





