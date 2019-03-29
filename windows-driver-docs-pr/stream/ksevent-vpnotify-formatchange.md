---
title: KSEVENT\_VPNOTIFY\_格式
description: KSEVENT\_VPNOTIFY\_格式事件用于传播事件，例如视频格式更改，从内核模式 DVD 解码器微型驱动程序的对 DirectShow 在用户模式下。
ms.assetid: 4c1757ec-1453-4aaa-b246-7c255e29310d
keywords:
- KSEVENT_VPNOTIFY_FORMATCHANGE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_VPNOTIFY_FORMATCHANGE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d05697309b7d8bfc3778d532482f8334fc9c1c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562949"
---
# <a name="kseventvpnotifyformatchange"></a>KSEVENT\_VPNOTIFY\_格式


KSEVENT\_VPNOTIFY\_格式事件用于传播事件，例如视频格式更改，从内核模式 DVD 解码器微型驱动程序的对 DirectShow 在用户模式下。

## <span id="ddk_ksevent_vpnotify_formatchange_ks"></span><span id="DDK_KSEVENT_VPNOTIFY_FORMATCHANGE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561937" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561937)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

微型驱动程序可检测视频格式，将更改从 640 x 480 的分辨率为 720 x 480 的示例中的更改。 用户模式组件必须此格式更改的通知，以便进行必要的操作可以 DirectShow 筛选器与 KsProxy 之间。

KsProxy 的 VPE 筛选器将通过此事件 （使用 Win32 API CreateEvent 创建） 的用户模式事件句柄传递给微型驱动程序，必须保存事件句柄。

更高版本，微型驱动程序设置此事件句柄，以通知 KsProxy VPE 筛选器，它会重新协商基于新的视频格式的连接。

KsProxy VPE 筛选器禁用事件通知的发送 IOCTL\_KS\_禁用\_事件输入/输出控制代码相同的事件句柄。 VPE 筛选器然后关闭的事件句柄。 微型驱动程序必须关闭的事件句柄。

有关 DirectShow 筛选器和 KsProxy 详细信息请参阅[内核流式处理代理](https://msdn.microsoft.com/library/windows/hardware/ff560877)。 有关处理流更改，如视频分辨率更改的详细信息请参阅[Stream 更改](https://msdn.microsoft.com/library/windows/hardware/ff568284)。

 

 





