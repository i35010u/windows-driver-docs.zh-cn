---
title: KSPROPERTY\_JACK\_DESCRIPTION2
description: KSPROPERTY\_JACK\_DESCRIPTION2 属性实现为一个 pin-wise 属性，可通过使用筛选器句柄。
ms.assetid: 6856060b-f735-4ed8-99bd-5896c87d581f
keywords:
- KSPROPERTY_JACK_DESCRIPTION2 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_DESCRIPTION2
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0102ac8139923676770f69a8ec01fc2ce44b4c03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566605"
---
# <a name="kspropertyjackdescription2"></a>KSPROPERTY\_JACK\_DESCRIPTION2


KSPROPERTY\_JACK\_DESCRIPTION2 属性实现为一个 pin-wise 属性，可通过使用筛选器句柄。

在 Windows 7 和更高版本的 Windows 操作系统中，可以在任何一个或多个物理插孔与相关联的桥插针上支持此属性。 KSPROPERTY\_JACK\_DESCRIPTION2 用于获得的状态和 jack 相关设备的功能。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>（通过筛选器句柄） 的 pin 工厂</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx)"><strong>KSMULTIPLE_ITEM</strong> </a>跟的数组<a href="ksjack-description2.md" data-raw-source="[&lt;strong&gt;KSJACK_DESCRIPTION2&lt;/strong&gt;](ksjack-description2.md)"> <strong>KSJACK_DESCRIPTION2</strong> </a>结构</p></td>
</tr>
</tbody>
</table>

 

属性值 （实例数据） 是 KSMULTIPLE\_项后, 跟数组 KSJACK\_DESCRIPTION2 结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_JACK\_DESCRIPTION2 属性请求返回 KSMULTIPLE\_项后跟一个数组*N* KSJACK\_DESCRIPTION2 结构，其中*N* = 的指定的桥 pin 与相关联的插孔。 以下列表显示属性请求返回的项。

KSMULTIPLE\_项。大小 = sizeof (KSMULTIPLE\_项) + N \* sizeof (KSJACK\_DESCRIPTION2)

KSMULTIPLE\_项。计数 = N

KSJACK\_DESCRIPTION2\[0\]

...

KSJACK\_DESCRIPTION2\[N-1\]

<a name="remarks"></a>备注
-------

每个 KSJACK\_DESCRIPTION2 结构必须仅包含一个 jack 有关的信息。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSJACK\_DESCRIPTION2**](ksjack-description2.md)

[KSMULTIPLE\_项](https://msdn.microsoft.com/library/windows/hardware/ff563441.aspx)

 

 






