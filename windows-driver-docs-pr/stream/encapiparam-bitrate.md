---
title: ENCAPIPARAM\_BITRATE
description: ENCAPIPARAM\_BITRATE
ms.assetid: a0fba9b3-7ce3-407d-b53f-fd54a50cbdcb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd0909ed9eab9fc349eb1125117c5a56c4472f5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384141"
---
# <a name="encapiparambitrate"></a>ENCAPIPARAM\_BITRATE


## <span id="ddk_encapiparam_bitrate_ks"></span><span id="DDK_ENCAPIPARAM_BITRATE_KS"></span>


ENCAPIPARAM\_比特率属性用于描述设备支持的位速率 （每秒位数）。

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
<th>Get</th>
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
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 VT\_UI4 单步执行范围中指定的设备支持的比特率**PropertyItem.Values**的成员[ **KSPROPERTY\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)结构。

### <a name="comments"></a>备注

有关如何使用此属性的示例，请参阅[编码器的代码示例](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-code-examples)。

微型驱动程序时需要提供一个静态**PropertyItem.Values**说明中的属性项或句柄基本支持的查询，并填充值。 微型驱动程序还必须指定此属性的默认值。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)， [ **VIDEOENCODER\_比特率\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)

 

 





