---
title: KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID
description: KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID 检索音频模块通知设备标识符 GUID。
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
ms.openlocfilehash: 445d17f5adbce2bd0da77d4b398a0b7b57497678
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832844"
---
# <a name="ksproperty_audiomodule_notification_device_id"></a>KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID


**KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID**检索音频模块通知设备标识符 GUID。

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
<td align="left"><p>筛选器句柄或固定句柄</p></td>
<td align="left"><p>KSPROPERTY</p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

返回的属性值是一个 GUID。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID**返回与音频模块通知设备标识符关联的 GUID。

如果筛选器句柄或固定句柄作为目标提供，则返回相同的设备 GUID 值。

<a name="remarks"></a>备注
-------

需要支持 KSPROPERTY\_AUDIOMODULE\_通知\_设备\_ID 才能使微型端口发出通知并将信息传递给音频模块客户端。 此 ID 的生存期与正在公开并对 Windows 音频堆栈激活的音频设备的生存期相关联。 可以通过筛选器或 pin 句柄发送属性，并将 KSPROPERTY 作为 DeviceIoControl 调用的输入缓冲区进行传递。

有关使用此 KSPROPERTY 的示例，请参阅 SYSVAD 音频驱动程序示例。

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

[**KSAUDIOMODULE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_notification)

 

 






