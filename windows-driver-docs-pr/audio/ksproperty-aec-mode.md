---
title: KSPROPERTY\_AEC\_MODE
description: KSPROPERTY\_AEC\_MODE 属性用于控制 AEC 节点的操作模式。 此为可选属性的 AEC 节点 (KSNODETYPE\_声学\_ECHO\_取消)。
ms.assetid: 79f0d655-4764-454f-8867-6cf1b5cedc82
keywords:
- KSPROPERTY_AEC_MODE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc1f71e2284382bef8ff2475c7515798a84b32b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563172"
---
# <a name="kspropertyaecmode"></a>KSPROPERTY\_AEC\_MODE


KSPROPERTY\_AEC\_MODE 属性用于控制 AEC 节点的操作模式。 此为可选的 AEC 节点的属性 ([**KSNODETYPE\_声学\_ECHO\_取消**](ksnodetype-acoustic-echo-cancel.md))。

## <span id="ddk_ksproperty_aec_mode_ks"></span><span id="DDK_KSPROPERTY_AEC_MODE_KS"></span>


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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型为 ULONG，可以从标头文件 Ksmedia.h 设置为以下模式常量之一：

-   AEC\_模式下\_传递\_THROUGH

    在直通模式下，在 AEC 节点允许捕获和呈现数据只需通过该节点，而无需修改。

-   AEC\_模式下\_一半\_双工

    AEC 算法运行在半双工模式下，在电话的操作类似。 在此模式下，每当本地人的语音卷级别比远程用户的更高时，设置为静音扬声器音量。

-   AEC\_模式下\_完整\_双工

    AEC 算法在全双工模式下运行。

默认值为直通模式。 当创建筛选器包含 AEC 节点或节点重置时，节点最初配置为在直通模式下操作。

在 Windows XP，AEC 算法的初始版本中的[AEC 系统筛选器](https://msdn.microsoft.com/library/windows/hardware/ff536174)使用不支持半双工模式。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AEC\_模式属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)

 

 






