---
title: KSPROPERTY\_VIDEODECODER\_状态
description: KSPROPERTY\_VIDEDECODER\_STATUS 属性从视频解码器中检索状态信息。 必须实现此属性。
ms.assetid: 1d8cb537-1d85-4536-bd75-33beea0f586d
keywords:
- KSPROPERTY_VIDEODECODER_STATUS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4d3c124bd1227434ea93b5f04cb008178fc274
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387440"
---
# <a name="kspropertyvideodecoderstatus"></a>KSPROPERTY\_VIDEODECODER\_状态


KSPROPERTY\_VIDEDECODER\_STATUS 属性从视频解码器中检索状态信息。 必须实现此属性。

## <span id="ddk_ksproperty_videodecoder_status_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_STATUS_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566061" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566061)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566061" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566061)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_VIDEODECODER\_状态\_S 结构，它指定视频解码设备，例如传入模拟信号中的行数的存在状态和是否锁定信号。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEODECODER\_状态\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566061)

 

 






