---
title: WDI_TLV_SET_POWER_DX_REASON
description: WDI_TLV_SET_POWER_DX_REASON 是一种 TLV，其中包含设置的 POWER Dx 的原因。
ms.assetid: 339F3461-3478-4C54-B6FB-9F5541859C76
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_POWER_DX_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d9a415898bb874ab68a7cad3b49e85cbbd34d88f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206155"
---
# <a name="wdi_tlv_set_power_dx_reason"></a>WDI \_ TLV \_ 设置 \_ POWER \_ DX \_ 原因


WDI \_ tlv \_ 设置 " \_ power \_ dx \_ 原因" 是包含设置的 power dx 原因的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x103

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>设置 power Dx 的原因。
<p>有效值是：</p>
<ul>
<li><p>WDI_SET_POWER_DX_REASON_SELETIVE_SUSPEND (1) </p>
<p>如果设置了此值，则表示在没有显式 <a href="wdi-tlv-enable-wake-events.md" data-raw-source="[&lt;strong&gt;WDI_TLV_ENABLE_WAKE_EVENTS&lt;/strong&gt;](wdi-tlv-enable-wake-events.md)"><strong>WDI_TLV_ENABLE_WAKE_EVENTS</strong></a>的任何感兴趣的外部事件上唤醒。 这是一种空闲的低功率，其中设备会以透明方式向最终用户公开。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/network/wdi-usb-remote-wake-sequence" data-raw-source="[WDI USB remote wake sequence](/windows-hardware/drivers/network/wdi-usb-remote-wake-sequence)">WDI USB 远程唤醒序列</a> 。</p></li>
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

 

