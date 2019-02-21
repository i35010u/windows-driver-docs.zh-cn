---
title: KSPROPERTY\_CROSSBAR\_PININFO
description: KSPROPERTY\_纵横制\_PININFO 属性检索包括等数据流方向，中等 GUID(s) 和 pin 类型设置 pin 所表示的物理连接的类型。
ms.assetid: d025b401-bc75-40d6-a367-1b98e065a48d
keywords:
- KSPROPERTY_CROSSBAR_PININFO 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_PININFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b188772c29797dc2e587af2354ed454e9c274c53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555722"
---
# <a name="kspropertycrossbarpininfo"></a>KSPROPERTY\_CROSSBAR\_PININFO


KSPROPERTY\_纵横制\_PININFO 属性检索包括等数据流方向，中等 GUID(s) 和 pin 类型设置 pin 所表示的物理连接的类型。 对于视频插针此属性还指示是否存在特定视频 pin 与关联的音频 pin。 必须实现此属性。

## <span id="ddk_ksproperty_crossbar_pininfo_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_PININFO_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<td><p>否</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565123" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565123)"><strong>KSPROPERTY_CROSSBAR_PININFO_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565123" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565123)"><strong>KSPROPERTY_CROSSBAR_PININFO_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_纵横制\_PININFO\_S 结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CROSSBAR\_PININFO\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565123)

 

 






