---
title: KSPROPERTY\_音频\_WAVERT\_当前\_编写\_位置
description: KSPROPERTY\_音频\_WAVERT\_当前\_编写\_属性请求指定当前以字节为单位写入 WaveRT 缓冲区的位置的位置。 卸载驱动程序可以使用此写位置信息以了解有效的数据量是 WaveRT 缓冲区中。
ms.assetid: 05C62E23-2460-4E92-BEE8-08D31A8BFD86
keywords:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c7dd2b4d0735c79cddb737f79fe060b7a7f237a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360567"
---
# <a name="kspropertyaudiowavertcurrentwriteposition"></a>KSPROPERTY\_音频\_WAVERT\_当前\_编写\_位置


KSPROPERTY\_音频\_WAVERT\_当前\_编写\_属性请求指定当前以字节为单位写入 WaveRT 缓冲区的位置的位置。 卸载驱动程序可以使用此写位置信息以了解有效的数据量是 WaveRT 缓冲区中。

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

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_WAVERT\_当前\_编写\_位置属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

若要更好地了解如何解释此属性请求提供的信息，假设一个循环缓冲区的大小为 n 个字节。 初始的写入位置之前写入任何数据，为 0。 数据写入到的倍数的块中的缓冲区[ **WAVEFORMATEX.nBlockAlign** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)字节。

例如，缓冲区可能包含 20 毫秒的 16 位 PCM 立体声，采样的数据 48000 Hz。 因此基于 nBlockAlign 成员的说明**WAVEFORMATEX**结构，请在此示例 nBlockAlign = 2 \* 16 / 8 = 4 个字节。 这意味着，缓冲区的长度会 48000 \* 20 / 1000年 = 960 帧或 960 \* 4 = 3840 字节。

第一个**设置**请求将指定的字节数已写入到缓冲区。 和"写入位置"以字节为单位表示，因为 1920年值将指定缓冲区大小的一半，而 3840 值将指示已满缓冲区大小。 若要确定新写入的字节数，使后续**设置**请求时，下面的伪代码演示如何执行计算：

``` syntax
if new write position > old write position:
     bytes written = new write position – old write position
if new write position < old write position, we’ve wrapped:
     bytes written = (new write position + buffer size) – old write position
if new write position = old write position, we’ve had a glitch
     log a "duplicate write position" glitch event
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)

 

 






