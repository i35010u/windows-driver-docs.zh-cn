---
title: PROPSETID \_ EXT \_ 设备
description: PROPSETID \_ EXT \_ 设备
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d3047f46260e669455cb5cd47652bf92031ee97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833957"
---
# <a name="propsetid_ext_device"></a>PROPSETID \_ EXT \_ 设备


## <span id="ddk_propsetid_ext_device_ks"></span><span id="DDK_PROPSETID_EXT_DEVICE_KS"></span>


PROPSETID \_ EXT \_ 设备属性集控制一个外部设备，如小型 DV 摄像机。

\_ *Ksmedia* 中的 KSPROPERTY EXTDEVICE 枚举指定此集的属性。

对此属性集的支持是可选的，只应由支持外部视频捕获设备的微型驱动程序实现。

[**KSPROPERTY \_ EXTDEVICE \_ ID**](ksproperty-extdevice-id.md)

[**KSPROPERTY \_ EXTDEVICE \_ 版本**](ksproperty-extdevice-version.md)

[**KSPROPERTY \_ EXTDEVICE \_ 电源 \_ 状态**](ksproperty-extdevice-power-state.md)

[**KSPROPERTY \_ EXTDEVICE \_ 端口**](ksproperty-extdevice-port.md)

[**KSPROPERTY \_ EXTDEVICE \_ 功能**](ksproperty-extdevice-capabilities.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMExtDevice** 接口 (参阅 Microsoft Windows SDK 中的 directshow 文档) 提供对此集的属性的访问权限。

 

 





