---
title: KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ 位置
description: KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ 位置属性请求指定 WAVERT 缓冲区的当前写入位置（以字节为单位）。 卸载驱动程序可以使用此写入位置信息来了解 WaveRT 缓冲区中的有效数据量。
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
ms.openlocfilehash: 6a11f2cfbfc520d2eb118d40e2b6a5bdbd3088b6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206923"
---
# <a name="ksproperty_audio_wavert_current_write_position"></a>KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ 位置


KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ 位置属性请求指定 WAVERT 缓冲区的当前写入位置（以字节为单位）。 卸载驱动程序可以使用此写入位置信息来了解 WaveRT 缓冲区中的有效数据量。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">获取</th>
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
<td align="left"><p>节点 via 引脚实例</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ 位置属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

为了更好地了解如何解释此属性请求提供的信息，假设有一个大小为 n 字节的循环缓冲区。 写入任何数据之前的初始写入位置为0。 数据将以块 [**WAVEFORMATEX**](/windows/desktop/api/mmreg/ns-mmreg-twaveformatex) 的倍数写入缓冲区。

例如，缓冲区包含16位 PCM 立体声数据的 20 ms，采样速度为 48000 Hz。 因此，根据 **WAVEFORMATEX** 结构的 nBlockAlign 成员的说明，在此示例中，nBlockAlign = 2 \* 16/8 = 4 个字节。 这意味着缓冲区的长度为 48000 \* 20/1000 = 960 帧，或 960 \* 4 = 3840 字节。

第一个 **Set** 请求将指定写入缓冲区的字节数。 由于 "写入位置" 以字节表示，因此值1920将指定缓冲区大小的一半，而值3840将指示完整的缓冲区大小。 若要确定写入的新字节数，为发出后续的 **Set** 请求，以下伪代码显示了如何执行计算：

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
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**WAVEFORMATEX**](/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)

 

