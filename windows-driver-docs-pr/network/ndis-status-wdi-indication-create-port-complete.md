---
title: NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE 指示 OID_WDI_TASK_CREATE_PORT 完成。
ms.assetid: 8d3cdac1-06d3-4a21-ac13-e6d789c6922e
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6467a26a4318bc1ca6a5e78940eb385c1e7c9dfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382910"
---
# <a name="ndisstatuswdiindicationcreateportcomplete"></a>NDIS\_状态\_WDI\_指示\_创建\_端口\_完成


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_创建\_端口\_完成以指示完成[OID\_WDI\_任务\_创建\_端口](oid-wdi-task-create-port.md)。

| Object |
|--------|
| Port   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                               | 允许多个 TLV 实例 | 可选 | 描述                         |
|--------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_PORT\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-port-attributes) |                                |          | 创建端口的属性。 |

 

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

 

 




