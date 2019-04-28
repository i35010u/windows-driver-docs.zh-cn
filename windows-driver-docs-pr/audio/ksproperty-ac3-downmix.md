---
title: KSPROPERTY\_AC3\_DOWNMIX
description: KSPROPERTY\_AC3\_DOWNMIX 属性指定是否需要被以适应扬声器配置的混合 AC-3 编码的流中的程序通道。
ms.assetid: 1d47f890-f7da-423f-adef-72b06a0f79d8
keywords:
- KSPROPERTY_AC3_DOWNMIX Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_DOWNMIX
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba14a887b9992fd7f1d60467b3652f283f4092b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333103"
---
# <a name="kspropertyac3downmix"></a>KSPROPERTY\_AC3\_DOWNMIX


KSPROPERTY\_AC3\_DOWNMIX 属性指定是否需要被以适应扬声器配置的混合 AC-3 编码的流中的程序通道。

## <span id="ddk_ksproperty_ac3_downmix_ks"></span><span id="DDK_KSPROPERTY_AC3_DOWNMIX_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537079" data-raw-source="[&lt;strong&gt;KSAC3_DOWNMIX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537079)"><strong>KSAC3_DOWNMIX</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSAC3\_DOWNMIX 结构，它指定的程序通道是否应被混合。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AC3\_DOWNMIX 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

如果通道正解码器的输出数小于 ac-3 流中编码的通道数 Downmixing 是必需的。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSAC3\_DOWNMIX**](https://msdn.microsoft.com/library/windows/hardware/ff537079)

 

 






