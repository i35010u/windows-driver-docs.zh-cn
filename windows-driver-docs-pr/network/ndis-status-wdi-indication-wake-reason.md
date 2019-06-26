---
title: NDIS_STATUS_WDI_INDICATION_WAKE_REASON
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_WAKE_REASON NIC 唤醒主机时指示唤醒原因。 唤醒原因用于调试目的，没有功能起作用。
ms.assetid: 5f2eb569-be1e-4f24-92f5-8405ffc7b061
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 11db75bfba89a8431f205f5c01151e32cd3c5dc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375196"
---
# <a name="ndisstatuswdiindicationwakereason"></a>NDIS\_状态\_WDI\_指示\_唤醒\_原因


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_唤醒\_NIC 唤醒主机时指示唤醒原因的理由。 唤醒原因用于调试目的，没有功能起作用。

| Object |
|--------|
| Port   |

 

当主机进入低功耗状态时，它将卸载到 NIC 的少数几个函数，而唤醒的 NIC。 发生唤醒事件时，NIC 将断言以主机中唤醒的唤醒中断行。 然后，主机将 D0 到 NIC （运行电源状态）。 一旦进入 D0 NIC 必须指示唤醒原因。

如果唤醒原因是唤醒数据包，NIC 还应包括唤醒数据包和匹配数据包唤醒模式 ID。 数据包封装为[ **WDI\_TLV\_指示\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-indication-wake-packet)。 此外应包括唤醒原因[ **WDI\_TLV\_指示\_唤醒\_数据包\_模式\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-indication-wake-packet-pattern-id)到指定将该数据包匹配的模式 ID。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                                      | 允许多个 TLV 实例 | 可选 | 描述                                                                                                 |
|-----------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_INDICATION\_WAKE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-indication-wake-reason)                         |                                |          | 唤醒原因。                                                                                            |
| [**WDI\_TLV\_指示\_唤醒\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-indication-wake-packet)                         |                                | X        | 唤醒数据包。                                                                                            |
| [**WDI\_TLV\_指示\_唤醒\_数据包\_模式\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-indication-wake-packet-pattern-id) |                                | X        | 唤醒数据包匹配的模式的 ID。 从模式的添加命令获取的 ID。 |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




