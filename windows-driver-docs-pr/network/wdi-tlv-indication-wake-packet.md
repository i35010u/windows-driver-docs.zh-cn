---
title: WDI_TLV_INDICATION_WAKE_PACKET
description: WDI_TLV_INDICATION_WAKE_PACKET 是包含 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 唤醒数据包 TLV。 WDI_WAKE_REASON_CODE 数据包唤醒原因时，状态必须包括在 WDI_TLV_INDICATION_WAKE_PACKET 中封装的唤醒数据包。
ms.assetid: 3C566FED-4594-403F-93D4-1CA6F2F655F9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_WAKE_PACKET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dd1dd12dd2fbbe85c4980a2c8370b674d6036767
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380759"
---
# <a name="wditlvindicationwakepacket"></a>WDI\_TLV\_指示\_唤醒\_数据包


WDI\_TLV\_指示\_唤醒\_数据包是包含有关唤醒数据包 TLV [NDIS\_状态\_WDI\_指示\_唤醒\_原因](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-wake-reason)。 唤醒原因时 WDI\_唤醒\_原因\_代码数据包状态必须包括唤醒数据包封装在 WDI\_TLV\_指示\_唤醒\_数据包。

## <a name="tlv-type"></a>TLV 类型


0x9D

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                       |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 唤醒数据包。 大小为接收平面内存版本将在正常所指示的数据包的大小的路径。 |

 

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

 

 




