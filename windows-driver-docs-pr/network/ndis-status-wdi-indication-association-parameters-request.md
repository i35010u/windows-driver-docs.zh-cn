---
title: NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST 请求关联参数 BSSIDs 一组主机中。
ms.assetid: 2c8aef86-bb4a-47c6-a839-eb14eb430a31
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f67524869a9ebd3660f7b6d3deb049dd1516c67b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366418"
---
# <a name="ndisstatuswdiindicationassociationparametersrequest"></a>NDIS\_状态\_WDI\_指示\_关联\_参数\_请求


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_关联\_参数\_向宿主请求 BSSIDs 一组的关联参数的请求。

| Object |
|--------|
| 端口   |

 

找到适合于基于当前设置关联的 BSS 条目时，适配器可以发送此指示。 收到此指示时，主机检查和关联参数是否可用，如果是这样，将其发送与[OID\_WDI\_设置\_关联\_参数](oid-wdi-set-association-parameters.md)。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                                             | 允许多个 TLV 实例 | 可选 | 描述                                   |
|------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_关联\_参数\_请求\_类型**](https://msdn.microsoft.com/library/windows/hardware/dn926131) |                                |          | 请求的关联参数的列表。 |
| [**WDI\_TLV\_BSS\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/dn926162)                                                           | X                              | X        | BSSIDs 的列表。                           |

 

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


[OID\_WDI\_TASK\_CONNECT](oid-wdi-task-connect.md)

 

 




