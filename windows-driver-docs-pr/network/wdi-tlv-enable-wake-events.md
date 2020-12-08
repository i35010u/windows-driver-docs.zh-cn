---
title: WDI_TLV_ENABLE_WAKE_EVENTS
description: WDI_TLV_ENABLE_WAKE_EVENTS 为 TLV，其中包含已启用的唤醒事件。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ENABLE_WAKE_EVENTS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 347d4e39ced04d76d9b2e4dcfb386eeebf439b04
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837889"
---
# <a name="wdi_tlv_enable_wake_events"></a>WDI \_ TLV \_ 启用 \_ 唤醒 \_ 事件


WDI \_ tlv \_ 启用 \_ 唤醒 \_ 事件是包含已启用的唤醒事件的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x60

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                                                          |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 使用 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)中所述的标志指定启用的 LAN 唤醒包模式。EnabledWoLPacketPatterns. |
| UINT32 | 使用 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)中所述的标志指定启用的协议卸载。EnabledProtocolOffloads.            |
| UINT32 | 使用 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)中所述的标志指定唤醒标志。WakeUpFlags.                                    |
| UINT32 | 使用 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)中所述的标志指定特定于媒体的唤醒事件。MediaSpecificWakeUpEvents.      |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

