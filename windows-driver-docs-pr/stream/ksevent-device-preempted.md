---
title: KSEVENT\_设备\_已占用
description: KSEVENT\_设备\_设备已被占用时，会触发已占用事件。
ms.assetid: A51B7109-AFBE-4849-9655-F913FB7851F1
keywords:
- KSEVENT_DEVICE_PREEMPTED 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_DEVICE_PREEMPTED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ab1390ddb04d81fe6aa2e685ba4f125a4fe799
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391715"
---
# <a name="kseventdevicepreempted"></a>KSEVENT\_设备\_已占用


**KSEVENT\_设备\_已占用**设备已被占用时，会触发事件。

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
<td><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在以下方案中触发抢占事件。

1.  最初只有一个照相机已连接到系统，和 Windows 应用流式处理视频从摄像机。
2.  第二个 Windows 应用请求捕获堆栈抢占的第一个应用的设备，并将控制权授予第二个应用。
3.  当发出此请求时，驱动程序将发送**KSEVENT\_设备\_已占用**到这两个 Windows 应用的事件。

## <a name="see-also"></a>请参阅


[**KSEVENT\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksevent_device)

[**KSEVENT\_DEVICE\_LOST**](ksevent-device-lost.md)

 

 






