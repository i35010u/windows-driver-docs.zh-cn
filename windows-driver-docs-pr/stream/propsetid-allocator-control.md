---
title: PROPSETID\_分配器\_控件
description: PROPSETID\_分配器\_控件
ms.assetid: a3e0a5e9-4357-4bc9-ba2a-098f344ed01e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9ebc2aed40b72029a07e7f06298cfbead9150be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563979"
---
# <a name="propsetidallocatorcontrol"></a>PROPSETID\_分配器\_控件


## <span id="ddk_propsetid_allocator_control_ks"></span><span id="DDK_PROPSETID_ALLOCATOR_CONTROL_KS"></span>


PROPSETID\_分配器\_控件属性设置控件的覆盖面上，例如视频端口和/或 Microsoft DirectDraw 表面分配。 设备控制的已分配 DirectDraw 图面数和/或视频缩放，且视频解码器不能，指示到覆盖 Mixer 应实现此集的属性。 覆盖 Mixer 使用此组的属性来控制 Microsoft DirectDraw 图面上分配和维度。

KSPROPERTY\_ALLOCATOR\_控件中的枚举*ksmedia.h*指定此集的属性。

支持设置此属性是可选的应仅通过使用覆盖面设备来实现。

[**KSPROPERTY\_ALLOCATOR\_控制\_遵循\_计数**](ksproperty-allocator-control-honor-count.md)

[**KSPROPERTY\_ALLOCATOR\_控制\_面\_大小**](ksproperty-allocator-control-surface-size.md)

[**KSPROPERTY\_ALLOCATOR\_控制\_捕获\_CAP**](ksproperty-allocator-control-capture-caps.md)

[**KSPROPERTY\_ALLOCATOR\_控制\_捕获\_交错**](ksproperty-allocator-control-capture-interleave.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

没有 DirectShow 界面提供访问此属性集。

 

 





