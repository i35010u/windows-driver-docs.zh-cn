---
title: WDI_TLV_ENABLE_WAKE_EVENTS
description: WDI_TLV_ENABLE_WAKE_EVENTS 是包含启用了的唤醒事件 TLV。
ms.assetid: 5F348D9A-5575-46EE-A524-687E9D030754
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ENABLE_WAKE_EVENTS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 749d4dd22b9446b23dd8674d9f33f56eb4224492
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380867"
---
# <a name="wditlvenablewakeevents"></a>WDI\_TLV\_启用\_唤醒\_事件


WDI\_TLV\_启用\_唤醒\_事件是包含启用了的唤醒事件 TLV。

## <a name="tlv-type"></a>TLV 类型


0x60

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                                                          |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 指定使用标志，如中所述的已启用的 LAN 唤醒数据包模式[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)。EnabledWoLPacketPatterns。 |
| UINT32 | 指定已启用的协议将卸载使用标志，如中所述[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)。EnabledProtocolOffloads。            |
| UINT32 | 指定使用标志，如中所述的唤醒标志[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)。WakeUpFlags。                                    |
| UINT32 | 指定特定于媒体的事件中所述使用标志唤醒[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)。MediaSpecificWakeUpEvents。      |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




