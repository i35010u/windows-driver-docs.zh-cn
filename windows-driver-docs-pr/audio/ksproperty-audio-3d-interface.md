---
title: KSPROPERTY\_AUDIO\_3D\_INTERFACE
description: KSPROPERTY\_音频\_3D\_接口属性指定要用于处理声音缓冲区中的数据的三维算法。
ms.assetid: 76c56e61-23ef-43ad-b66b-2412fd247b6e
keywords:
- KSPROPERTY_AUDIO_3D_INTERFACE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_3D_INTERFACE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70cb661794ed4615c87426533ae566a94b7904cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556020"
---
# <a name="kspropertyaudio3dinterface"></a>KSPROPERTY\_AUDIO\_3D\_INTERFACE


KSPROPERTY\_音频\_3D\_接口属性指定要用于处理声音缓冲区中的数据的三维算法。

## <span id="ddk_ksproperty_audio_3d_interface_ks"></span><span id="DDK_KSPROPERTY_AUDIO_3D_INTERFACE_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定的三维算法的 GUID。 此值可以是以下 Guid 从标头文件 Dsound.h 之一：

-   DS3DALG\_默认

-   DS3DALG\_否\_虚拟化

-   DS3DALG\_HRTF\_FULL

-   DS3DALG\_HRTF\_光

有关这些 Guid 的详细信息，请参阅的说明**guid3dAlgorithm** DSBUFFERDESC 结构中 Microsoft Windows SDK 文档中的成员。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_3D\_接口属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_3D\_EFFECTS**](ksnodetype-3d-effects.md)

 

 






