---
title: PROPSETID \_ 分配器 \_ 控件
description: PROPSETID \_ 分配器 \_ 控件
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d54f04c2c1e183d072c1cb18c76097847be3b41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790143"
---
# <a name="propsetid_allocator_control"></a>PROPSETID \_ 分配器 \_ 控件


## <span id="ddk_propsetid_allocator_control_ks"></span><span id="DDK_PROPSETID_ALLOCATOR_CONTROL_KS"></span>


PROPSETID \_ 分配器 \_ 控件属性集控制覆盖图面的分配，如视频端口和/或 Microsoft DirectDraw 表面。 控制分配的 DirectDraw 表面数和/或向重叠混音器指示无法在视频解码器上进行视频缩放的设备应实现此集的属性。 覆盖混音器使用此集的属性来控制 Microsoft DirectDraw surface 分配和维度。

\_Ksmedia 中的 KSPROPERTY 分配器 \_ 控件枚举指定此集的属性。 *ksmedia.h*

对此属性集的支持是可选的，只应由使用重叠面的设备来实现。

[**KSPROPERTY \_ 分配器 \_ 控制 \_ 服从 \_ 计数**](ksproperty-allocator-control-honor-count.md)

[**KSPROPERTY \_ 分配器 \_ 控件 \_ 表面 \_ 大小**](ksproperty-allocator-control-surface-size.md)

[**KSPROPERTY \_ 分配器 \_ 控件 \_ 捕获 \_ CAP**](ksproperty-allocator-control-capture-caps.md)

[**KSPROPERTY \_ 分配器 \_ 控件 \_ 捕获 \_ 交错**](ksproperty-allocator-control-capture-interleave.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

没有可提供对此属性集的访问的 DirectShow 接口。

 

 





