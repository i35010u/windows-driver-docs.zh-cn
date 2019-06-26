---
title: KSPROPERTY\_音频\_WAVERT\_当前\_编写\_LASTBUFFER\_位置
description: KSPROPERTY\_音频\_WAVERT\_当前\_编写\_LASTBUFFER\_POSITION 属性用于指示音频缓冲区中的最后一个有效字节。
ms.assetid: 01EC2F29-D30A-4017-841F-8443D7C4BCF6
keywords:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2dcd5e64408dc015b12e7d5f7f4076689b0757f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358875"
---
# <a name="kspropertyaudiowavertcurrentwritelastbufferposition"></a>KSPROPERTY\_音频\_WAVERT\_当前\_编写\_LASTBUFFER\_位置


KSPROPERTY\_音频\_WAVERT\_当前\_编写\_LASTBUFFER\_POSITION 属性用于指示音频缓冲区中的最后一个有效字节。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>通过 Pin 实例的节点</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值是类型为 ULONG，代表 WaveRT 音频缓冲区中的最后一个有效字节。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_WAVERT\_当前\_编写\_LASTBUFFER\_位置属性请求将返回状态\_成功以指示它已完成已成功。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

如果客户端应用程序使用 KSPROPERTY\_类型\_BASICSUPPORT 标志时它将发送 KSPROPERTY\_音频\_WAVERT\_当前\_编写\_LASTBUFFER\_对音频驱动程序和状态的位置属性请求\_返回成功，它确认该驱动程序支持新添加的 KSPROPERTY\_音频\_WAVERT\_当前\_编写\_LASTBUFFER\_POSITION 属性。

当客户端应用程序执行到要卸载的流的音频驱动程序处理的音频缓冲区的最后一个写入操作时，音频驱动程序调用[ **SetStreamCurrentWritePositionForLastBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)方法。 **SetStreamCurrentWritePositionForLastBuffer**方法指示最后一个缓冲区中的"写入位置"，在流中。 请注意，可以仅部分填充此最后一个缓冲区。

如果开发的没有设计成可与音频端口类驱动程序 (Portcls) 的音频驱动程序，则必须实现此属性处理程序新 KS 属性。

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
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**SetStreamCurrentWritePositionForLastBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)

 

 






