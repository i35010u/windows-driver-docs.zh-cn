---
title: KSPROPERTY\_AUDIOMODULE\_命令
description: KSPROPERTY\_AUDIOMODULE\_命令属性是一个命令属性，用于获取和设置有关硬件（固定句柄）或软件缓存（筛选器句柄）的缓冲区和说明。
ms.assetid: 90C69481-A3DF-4801-8733-C417950880E5
keywords:
- KSPROPERTY_AUDIOMODULE_COMMAND 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_COMMAND
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1626793bee02a406cc062e0a3b1b9e5c376403e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832866"
---
# <a name="ksproperty_audiomodule_command"></a>KSPROPERTY\_AUDIOMODULE\_命令


**KSPROPERTY\_AUDIOMODULE\_命令**属性是一个命令属性，用于获取和设置有关硬件（固定句柄）或软件缓存（筛选器句柄）的缓冲区和说明。

*设置*值作为命令的一部分提供。 使用*Get*时，它将返回此命令的结果。

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>筛选器或固定</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property" data-raw-source="[&lt;strong&gt;KSAUDIOMODULE_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)"><strong>KSAUDIOMODULE_PROPERTY</strong></a> + [可选的自定义模块参数]</p></td>
<td align="left"><p>尚未</p></td>
</tr>
</tbody>
</table>

 

属性值类型为 undefined。 实施者可以创建特定于模块的自定义命令结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOMODULE\_命令**返回音频模块命令特定信息。

<a name="remarks"></a>备注
-------

支持**KSPROPERTY\_AUDIOMODULE\_COMMAND**属性允许音频模块客户端发送自定义命令，以便查询和设置音频模块上的参数。 可以通过筛选器或 pin 句柄发送属性，并将[**KSAUDIOMODULE\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)传递为 DeviceIoControl 调用的输入缓冲区。 在输入缓冲区中，客户端可以选择立即发送与**KSAUDIOMODULE\_属性**相邻的附加信息，以发送自定义命令。

有关音频模块的详细信息，请参阅[实现音频模块发现](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)。

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
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>Windows 10 版本1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

 

 






