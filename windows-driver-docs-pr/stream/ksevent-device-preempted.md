---
title: KSEVENT \_ 设备已被 \_ 抢占
description: '\_ \_ 设备被抢占后，将触发 KSEVENT 设备被抢占事件。'
keywords:
- KSEVENT_DEVICE_PREEMPTED 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_DEVICE_PREEMPTED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a30b69c3f18dc670f32d4d5cb74e1bbf3687ff6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813449"
---
# <a name="ksevent_device_preempted"></a>KSEVENT \_ 设备已被 \_ 抢占


设备被抢占后，将触发 **KSEVENT \_ 设备被 \_ 抢占** 事件。

## <span id="ddk_ksevent_vidcap_auto_update_ks"></span><span id="DDK_KSEVENT_VIDCAP_AUTO_UPDATE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th>获取</th>
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
<td><p>筛选器</p></td>
<td><p><a href="/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在以下情况下，将触发抢占事件。

1.  最初，系统只会将一个相机连接到系统，而 Windows 应用则会从相机流式传输视频。
2.  第二个 Windows 应用请求捕获堆栈从第一个应用中抢占设备并为第二个应用授予控制权。
3.  发出此请求时，驱动程序会将 **KSEVENT \_ 设备 \_ 抢先** 事件发送到两个 Windows 应用。

## <a name="see-also"></a>请参阅


[**KSEVENT \_ 设备**](/windows-hardware/drivers/ddi/ks/ne-ks-ksevent_device)

[**KSEVENT \_ 设备 \_ 丢失**](ksevent-device-lost.md)

