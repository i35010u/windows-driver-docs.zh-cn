---
title: ENCAPIPARAM \_ 比特率 \_ 模式
description: ENCAPIPARAM \_ 比特率 \_ 模式
ms.assetid: d7e82483-bee3-44bd-9066-c2877130a1f9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebddf4615ac29b94238df4001106b0804be8cac0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187416"
---
# <a name="encapiparam_bitrate_mode"></a>ENCAPIPARAM \_ 比特率 \_ 模式


## <span id="ddk_encapiparam_bitrate_mode_ks"></span><span id="DDK_ENCAPIPARAM_BITRATE_MODE_KS"></span>


ENCAPIPARAM \_ 比特率属性用于描述设备的编码模式。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 \_ 在[**KSPROPERTY \_ 集**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)结构的**PROPERTYITEM**成员中指定的 VT I4 值，其中包含来自[**VIDEOENCODER \_ 比特率 \_ 模式**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)枚举的不同支持值列表。

### <a name="comments"></a>注释

有关如何使用此属性的示例，请参阅 [编码器代码示例](./encoder-code-examples.md)。

微型驱动程序是在属性项中提供静态 **PropertyItem** 说明或处理基本支持查询并填充中的值所必需的。 微型驱动程序还必须指定此属性的默认值。

### <a name="requirements"></a>要求

**标头：** 在 *ksmedia*中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)， [ **VIDEOENCODER \_ 比特率 \_ 模式**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

