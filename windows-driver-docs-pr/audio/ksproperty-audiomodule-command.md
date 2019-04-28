---
title: KSPROPERTY\_AUDIOMODULE\_命令
description: KSPROPERTY\_AUDIOMODULE\_COMMAND 属性是一个用于获取和设置缓冲区和说明 （固定句柄） 的硬件或软件缓存 （筛选器句柄） 上的命令属性。
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
ms.openlocfilehash: 52c6bf7350cd61659df8128986067d5d04029dfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332766"
---
# <a name="kspropertyaudiomodulecommand"></a>KSPROPERTY\_AUDIOMODULE\_命令


**KSPROPERTY\_AUDIOMODULE\_命令**属性是一个用于获取和设置缓冲区和说明 （固定句柄） 的硬件或软件缓存 （筛选器句柄） 上的命令属性。

*设置*命令的一部分提供值。 当*获取*是使用，它将返回此命令的结果。

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
<td align="left"><p>否</p></td>
<td align="left"><p>筛选器或 Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt808139" data-raw-source="[&lt;strong&gt;KSAUDIOMODULE_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt808139)"><strong>KSAUDIOMODULE_PROPERTY</strong> </a> + [可选自定义模块参数]</p></td>
<td align="left"><p>未定义</p></td>
</tr>
</tbody>
</table>

 

属性值类型未定义。 实施者可以创建一个模块特定自定义命令结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOMODULE\_命令**返回音频模块命令特定信息。

<a name="remarks"></a>备注
-------

为支持**KSPROPERTY\_AUDIOMODULE\_命令**属性允许音频模块客户端发送自定义命令来查询和设置音频模块的参数。 可以通过筛选器或 pin 句柄发送该属性和一个[ **KSAUDIOMODULE\_属性**](https://msdn.microsoft.com/library/windows/hardware/mt808139)作为 DeviceIoControl 调用的输入缓冲区传递。 客户端可以根据需要发送的其他信息立即旁边**KSAUDIOMODULE\_属性**将自定义命令发送到输入缓冲区中。

有关音频模块的详细信息，请参阅[实现音频模块发现](https://msdn.microsoft.com/windows/hardware/drivers/audio/implementing-audio-module-communication)。

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
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 10，版本 1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

 

 






