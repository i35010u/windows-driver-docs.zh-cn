---
title: WDI_TLV_ENABLE_WAKE_EVENTS
description: WDI_TLV_ENABLE_WAKE_EVENTS 是包含已启用的唤醒事件的 TLV。
ms.assetid: 5F348D9A-5575-46EE-A524-687E9D030754
ms.date: 07/18/2017
keywords:
- WDI_TLV_ENABLE_WAKE_EVENTS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bedd644ca8db67bdb6d1a530a4dfb46d9a83db04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834102"
---
# <a name="wdi_tlv_enable_wake_events"></a>WDI\_TLV\_启用\_唤醒\_事件


WDI\_TLV\_启用\_唤醒\_事件是包含已启用的唤醒事件的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x60

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                          |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 使用[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)中所述的标志指定启用的 LAN 唤醒包模式。EnabledWoLPacketPatterns. |
| UINT32 | 使用[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)中所述的标志指定启用的协议卸载。EnabledProtocolOffloads.            |
| UINT32 | 使用[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)中所述的标志指定唤醒标志。WakeUpFlags.                                    |
| UINT32 | 使用[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)中所述的标志指定特定于媒体的唤醒事件。MediaSpecificWakeUpEvents.      |

 

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
<td><p>Windows 10</p></td>
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

 

 




