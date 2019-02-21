---
title: WDI_TLV_SET_POWER_DX_REASON
description: WDI_TLV_SET_POWER_DX_REASON 是 TLV 包含集 power Dx 的原因。
ms.assetid: 339F3461-3478-4C54-B6FB-9F5541859C76
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_POWER_DX_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fdc4a0e25ae474c0fa3be35debba07661b91ed09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534671"
---
# <a name="wditlvsetpowerdxreason"></a>WDI\_TLV\_SET\_POWER\_DX\_REASON


WDI\_TLV\_设置\_POWER\_DX\_原因是包含集 power Dx 原因 TLV。

## <a name="tlv-type"></a>TLV 类型


0x103

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>设置 power Dx 的原因。
<p>有效值包括：</p>
<ul>
<li><p>WDI_SET_POWER_DX_REASON_SELETIVE_SUSPEND (1)</p>
<p>当设置此值时，则意味着唤醒上任何有趣的外部事件，而无需显式<a href="wdi-tlv-enable-wake-events.md" data-raw-source="[&lt;strong&gt;WDI_TLV_ENABLE_WAKE_EVENTS&lt;/strong&gt;](wdi-tlv-enable-wake-events.md)"> <strong>WDI_TLV_ENABLE_WAKE_EVENTS</strong></a>。 这是空闲的低能耗其中设备函数以透明方式向最终用户，就好像 D0 中一样。 请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/mt269159" data-raw-source="[WDI USB remote wake sequence](https://msdn.microsoft.com/library/windows/hardware/mt269159)">WDI USB 远程唤醒序列</a>有关详细信息。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




