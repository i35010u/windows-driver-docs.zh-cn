---
title: NDIS_STATUS_WDI_INDICATION_WAKE_REASON
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_WAKE_REASON NIC 唤醒主机时指示唤醒原因。 唤醒原因用于调试目的，没有功能起作用。
ms.assetid: 5f2eb569-be1e-4f24-92f5-8405ffc7b061
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 48459164e04bdfdfe304b7da4b506acd624ec82a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323255"
---
# <a name="ndisstatuswdiindicationwakereason"></a>NDIS\_状态\_WDI\_指示\_唤醒\_原因


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_唤醒\_NIC 唤醒主机时指示唤醒原因的理由。 唤醒原因用于调试目的，没有功能起作用。

| Object |
|--------|
| 端口   |

 

当主机进入低功耗状态时，它将卸载到 NIC 的少数几个函数，而唤醒的 NIC。 发生唤醒事件时，NIC 将断言以主机中唤醒的唤醒中断行。 然后，主机将 D0 到 NIC （运行电源状态）。 一旦进入 D0 NIC 必须指示唤醒原因。

如果唤醒原因是唤醒数据包，NIC 还应包括唤醒数据包和匹配数据包唤醒模式 ID。 数据包封装为[ **WDI\_TLV\_指示\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/dn897833)。 此外应包括唤醒原因[ **WDI\_TLV\_指示\_唤醒\_数据包\_模式\_ID** ](https://msdn.microsoft.com/library/windows/hardware/dn897832)到指定将该数据包匹配的模式 ID。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                                      | 允许多个 TLV 实例 | 可选 | 描述                                                                                                 |
|-----------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_INDICATION\_WAKE\_REASON**](https://msdn.microsoft.com/library/windows/hardware/dn897834)                         |                                |          | 唤醒原因。                                                                                            |
| [**WDI\_TLV\_指示\_唤醒\_数据包**](https://msdn.microsoft.com/library/windows/hardware/dn897833)                         |                                | X        | 唤醒数据包。                                                                                            |
| [**WDI\_TLV\_指示\_唤醒\_数据包\_模式\_ID**](https://msdn.microsoft.com/library/windows/hardware/dn897832) |                                | X        | 唤醒数据包匹配的模式的 ID。 从模式的添加命令获取的 ID。 |

 

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

 

 




