---
title: KSEVENT \_ VPNOTIFY \_ FORMATCHANGE
description: KSEVENT \_ VPNOTIFY \_ FORMATCHANGE 事件用于在用户模式下将事件（如视频格式更改）从内核模式 DVD 解码器微型驱动程序传播到 DirectShow。
ms.assetid: 4c1757ec-1453-4aaa-b246-7c255e29310d
keywords:
- KSEVENT_VPNOTIFY_FORMATCHANGE 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_VPNOTIFY_FORMATCHANGE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68088d89178ffd26f975101d7a86e9f697dcb5d1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186145"
---
# <a name="ksevent_vpnotify_formatchange"></a>KSEVENT \_ VPNOTIFY \_ FORMATCHANGE


KSEVENT \_ VPNOTIFY \_ FORMATCHANGE 事件用于在用户模式下将事件（如视频格式更改）从内核模式 DVD 解码器微型驱动程序传播到 DirectShow。

## <span id="ddk_ksevent_vpnotify_formatchange_ks"></span><span id="DDK_KSEVENT_VPNOTIFY_FORMATCHANGE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

微型驱动程序可以检测视频格式的变化，例如，分辨率从640x480 更改为720x480。 用户模式组件必须收到此格式更改的通知，以便在 DirectShow 筛选器和 KsProxy 之间发生必要的操作。

KsProxy 的 VPE 筛选器通过此事件将使用 Win32 API CreateEvent) 创建的用户模式事件句 (柄传递到微型驱动程序，这必须保存事件句柄。

稍后，微型驱动程序将设置此事件句柄，通知 KsProxy VPE 筛选器，该筛选器将基于新的视频格式重新协商连接。

KsProxy VPE 筛选器通过 \_ \_ \_ 使用相同事件句柄发送 IOCTL KS 禁用事件 i/o 控制代码来禁用事件通知。 然后，将由 VPE 筛选器关闭该事件句柄。 微型驱动程序不得关闭事件句柄。

有关 DirectShow 筛选器和 KsProxy 的详细信息，请参阅 [内核流式处理代理](/windows-hardware/drivers/ddi/_stream/index)。 有关处理流更改的详细信息（如视频分辨率更改），请参阅 [流更改](./stream-changes.md)。

 

