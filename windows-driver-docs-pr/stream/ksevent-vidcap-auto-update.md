---
title: KSEVENT\_VIDCAP\_AUTO\_UPDATE
description: KSEVENT\_VIDCAP\_自动\_属性值更改时触发更新事件。
ms.assetid: dd7e665f-104d-4276-94aa-62d64faba69d
keywords:
- KSEVENT_VIDCAP_AUTO_UPDATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_VIDCAP_AUTO_UPDATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c748d84df8716cb1c37d29fc63953df482f57029
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324807"
---
# <a name="kseventvidcapautoupdate"></a>KSEVENT\_VIDCAP\_AUTO\_UPDATE


KSEVENT\_VIDCAP\_自动\_属性值更改时触发更新事件。

## <span id="ddk_ksevent_vidcap_auto_update_ks"></span><span id="DDK_KSEVENT_VIDCAP_AUTO_UPDATE_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561744" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561744)"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果用户翻转开关在设备上更改属性值，则通知此事件可能会注册客户端。 对于可用于此事件，硬件实现必须提供此功能的支持。

有关 DirectShow 筛选器和 KsProxy 详细信息请参阅[内核流式处理代理](https://msdn.microsoft.com/library/windows/hardware/ff560877)。

 

 





