---
title: KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID
description: KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID 检索音频模块通知设备标识符的 GUID。
ms.assetid: CD9C5FCD-FB2A-4B21-A15E-BA520C3311A7
keywords:
- KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e73e5d6fc275536e674a51013582ccdf1f6e0e82
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358823"
---
# <a name="kspropertyaudiomodulenotificationdeviceid"></a>KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID


**KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID**检索音频模块通知设备标识符的 GUID。

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
<td align="left"><p>筛选器句柄或 Pin 句柄</p></td>
<td align="left"><p>KSPROPERTY</p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

返回的属性值是一个 GUID。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID**返回与音频模块通知设备标识符关联的 GUID。

如果筛选器句柄或 pin 句柄提供作为目标，则返回相同的设备的 GUID 值。

<a name="remarks"></a>备注
-------

支持 KSPROPERTY\_AUDIOMODULE\_通知\_设备\_时需要启用信号通知微型端口，并将信息传递到音频模块的客户端 ID。 此 ID 的生存期取决于正在公开和活动到 Windows 音频堆栈的音频设备的生存期。 可以通过筛选器或 pin 句柄发送该属性，并作为 DeviceIoControl 调用的输入缓冲区传递 KSPROPERTY。

使用此 KSPROPERTY 的示例请参阅 SYSVAD 音频驱动程序示例。

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

[**KSAUDIOMODULE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_notification)

 

 






