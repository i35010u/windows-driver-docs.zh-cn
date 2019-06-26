---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_批处理
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_批处理属性指定的批处理模式下设置为三维侦听器。
ms.assetid: 370191f8-e5a2-40f0-a979-c14cf7f44756
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5569999e22d55869955dfb1e7b193f7cb337a5fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361031"
---
# <a name="kspropertydirectsound3dlistenerbatch"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_批处理


KSPROPERTY\_DIRECTSOUND3DLISTENER\_批处理属性指定的批处理模式下设置为三维侦听器。

## <span id="ddk_ksproperty_directsound3dlistener_batch_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值的类型 BOOL 和指定的批处理模式下设置：

-   当此属性的值是 **，则返回 TRUE**，微型端口驱动程序应缓存对侦听程序属性的所有更改和关联的缓冲区的所有属性。

-   值是何时**FALSE**，对侦听程序属性和缓冲区属性的更改会立即生效。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DLISTENER\_批处理属性请求返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性时从过渡 **，则返回 TRUE**到**FALSE**微型端口驱动程序应立即所有缓存的属性生效。 如果可能，缓存的任何属性应放入效果同时。

有关三维侦听器的批处理模式下设置的详细信息，请参阅的说明**IDirectSound3DListener::CommitDeferredSettings** Microsoft Windows SDK 文档中的方法。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






