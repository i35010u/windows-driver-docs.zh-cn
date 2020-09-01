---
title: ENCAPIPARAM \_ 峰值 \_ 比特率
description: ENCAPIPARAM \_ 峰值 \_ 比特率
ms.assetid: 444a20e0-f3af-4dbc-9272-44e992e059e8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e77586dabcf8f45f8251dec29d4c4ca53233c42
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187419"
---
# <a name="encapiparam_peak_bitrate"></a>ENCAPIPARAM \_ 峰值 \_ 比特率


## <span id="ddk_encapiparam_peak_bitrate_ks"></span><span id="DDK_ENCAPIPARAM_PEAK_BITRATE_KS"></span>


ENCAPIPARAM \_ 比特率属性用于描述设备的受支持的高峰比特率 (每秒位数) 范围。

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
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 \_ 在[**KSPROPERTY \_ 集**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)结构的**PropertyItem**成员中指定的设备的高峰比特率 UI4。

### <a name="comments"></a>注释

微型驱动程序是在属性项中提供静态 **PropertyItem** 说明或处理基本支持查询并填充中的值所必需的。 微型驱动程序还必须指定此属性的默认值。

### <a name="requirements"></a>要求

**标头：** 在 *ksmedia*中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)， [ **VIDEOENCODER \_ 比特率 \_ 模式**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

