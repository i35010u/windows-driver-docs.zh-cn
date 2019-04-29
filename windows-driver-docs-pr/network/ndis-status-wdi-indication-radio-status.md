---
title: NDIS_STATUS_WDI_INDICATION_RADIO_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_RADIO_STATUS 指示适配器的单选状态中的更改。
ms.assetid: c2f90a52-ce55-4819-a66a-cfcc591cb3e9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_RADIO_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bb01101302e3e06b4c5abc9a852743726a394a1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361058"
---
# <a name="ndisstatuswdiindicationradiostatus"></a>NDIS\_状态\_WDI\_指示\_单选\_状态


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_单选\_状态，以指示适配器的单选状态中的更改。 软件无线电更改触发的主机，以及由适配器检测到硬件单选状态更改时发送此未经请求的指示。

| Object |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                  | 允许多个 TLV 实例 | 可选 | 描述                                              |
|-----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI\_TLV\_RADIO\_STATE**](https://msdn.microsoft.com/library/windows/hardware/dn898043) |                                |          | 在硬件和软件无线电当前状态。 |

 

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

## <a name="see-also"></a>请参阅


[WDI\_TASK\_SET\_RADIO\_STATE](oid-wdi-task-set-radio-state.md)

 

 




