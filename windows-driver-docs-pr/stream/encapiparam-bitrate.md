---
title: ENCAPIPARAM\_比特率
description: ENCAPIPARAM\_比特率
ms.assetid: a0fba9b3-7ce3-407d-b53f-fd54a50cbdcb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c1c0e3493c70a15bd7e743a826e4ba17cae545a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843209"
---
# <a name="encapiparam_bitrate"></a>ENCAPIPARAM\_比特率


## <span id="ddk_encapiparam_bitrate_ks"></span><span id="DDK_ENCAPIPARAM_BITRATE_KS"></span>


ENCAPIPARAM\_比特率属性用于描述设备支持的比特率（每秒位数）。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 UI4 在[**KSPROPERTY\_集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)结构的**PropertyItem**成员中指定的、由设备支持的比特率的 VT\_。

### <a name="comments"></a>备注

有关如何使用此属性的示例，请参阅[编码器代码示例](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-code-examples)。

微型驱动程序是在属性项中提供静态**PropertyItem**说明或处理基本支持查询并填充中的值所必需的。 微型驱动程序还必须指定此属性的默认值。

### <a name="requirements"></a>要求

**标头：** 在*ksmedia*中声明。 包括*ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)， [ **VIDEOENCODER\_比特率\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 





