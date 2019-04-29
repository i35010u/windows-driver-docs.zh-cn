---
title: ENCAPIPARAM\_BITRATE\_MODE
description: ENCAPIPARAM\_BITRATE\_MODE
ms.assetid: d7e82483-bee3-44bd-9066-c2877130a1f9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18593d48db168d4a891b8fbe4691c956cbcaa9a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363669"
---
# <a name="encapiparambitratemode"></a>ENCAPIPARAM\_BITRATE\_MODE


## <span id="ddk_encapiparam_bitrate_mode_ks"></span><span id="DDK_ENCAPIPARAM_BITRATE_MODE_KS"></span>


ENCAPIPARAM\_比特率属性用于描述设备的编码模式。

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
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 VT\_I4 中指定的值**PropertyItem.Values**的成员[ **KSPROPERTY\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff565617)使用离散的受支持的值列表的结构[ **VIDEOENCODER\_比特率\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff568695)枚举。

### <a name="comments"></a>备注

有关如何使用此属性的示例，请参阅[编码器的代码示例](https://msdn.microsoft.com/library/windows/hardware/ff559532)。

微型驱动程序时需要提供一个静态**PropertyItem.Values**说明中的属性项或句柄基本支持的查询，并填充值。 微型驱动程序还必须指定此属性的默认值。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)， [ **VIDEOENCODER\_比特率\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff568695)

 

 





