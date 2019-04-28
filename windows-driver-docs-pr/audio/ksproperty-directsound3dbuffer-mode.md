---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_MODE
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_模式属性指定的三维声音缓冲区处理模式。
ms.assetid: a3b15544-c534-47ea-a02e-5c8f9ccee414
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MODE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad2939cdd1ea059f790c3615c2aebc1c546b7a4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332789"
---
# <a name="kspropertydirectsound3dbuffermode"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_MODE


KSPROPERTY\_DIRECTSOUND3DBUFFER\_模式属性指定的三维声音缓冲区处理模式。

## <span id="ddk_ksproperty_directsound3dbuffer_mode_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_MODE_KS"></span>


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
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是类型为 ULONG，它指定声音缓冲区的处理模式。 模式可以具有标头文件 Dsound.h 中定义的以下值之一：

-   DS3DMODE\_正常

-   DS3DMODE\_HEADRELATIVE

-   DS3DMODE\_禁用

这些参数的含义是 Microsoft Windows SDK 文档中所述。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DBUFFER\_模式属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 3D 缓冲区的处理模式的更多信息，请参阅 Windows SDK 文档中的以下：

-   **DwMode** DS3DBUFFER 结构中的成员。

-   **IDirectSound3DBuffer::GetMode**并**IDirectSound3DBuffer::SetMode**方法。

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

 

 






