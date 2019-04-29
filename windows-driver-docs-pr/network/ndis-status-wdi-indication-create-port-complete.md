---
title: NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE 指示 OID_WDI_TASK_CREATE_PORT 完成。
ms.assetid: 8d3cdac1-06d3-4a21-ac13-e6d789c6922e
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_CREATE_PORT_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 32f09995ff9fff702ba366e672aaad6e64166377
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366395"
---
# <a name="ndisstatuswdiindicationcreateportcomplete"></a>NDIS\_状态\_WDI\_指示\_创建\_端口\_完成


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_创建\_端口\_完成以指示完成[OID\_WDI\_任务\_创建\_端口](oid-wdi-task-create-port.md)。

| Object |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                               | 允许多个 TLV 实例 | 可选 | 描述                         |
|--------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_PORT\_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/dn898038) |                                |          | 创建端口的属性。 |

 

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

 

 




