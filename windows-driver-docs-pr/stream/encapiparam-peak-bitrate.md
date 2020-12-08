---
title: ENCAPIPARAM \_ 峰值 \_ 比特率
description: ENCAPIPARAM \_ 峰值 \_ 比特率
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77cc90c7cb9fea470d84a2d8a41967fb41fd15f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782057"
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

 

 (操作数据) 的属性值是 \_ 在 [**KSPROPERTY \_ 集**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)结构的 **PropertyItem** 成员中指定的设备的高峰比特率 UI4。

### <a name="comments"></a>注释

微型驱动程序是在属性项中提供静态 **PropertyItem** 说明或处理基本支持查询并填充中的值所必需的。 微型驱动程序还必须指定此属性的默认值。

### <a name="requirements"></a>要求

**标头：** 在 *ksmedia* 中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)， [ **VIDEOENCODER \_ 比特率 \_ 模式**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

