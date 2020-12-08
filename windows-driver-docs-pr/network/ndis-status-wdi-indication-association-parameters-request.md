---
title: NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST 从主机请求一组 BSSIDs 的关联参数。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3d585d9c90da1bf1b598cdf1a9ac4c4be1bdde11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837147"
---
# <a name="ndis_status_wdi_indication_association_parameters_request"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 关联 \_ 参数 \_ 请求


微型端口驱动程序使用 NDIS \_ STATUS \_ WDI \_ 指示 \_ 关联 \_ 参数 \_ 请求来请求主机上一组 BSSIDs 的关联参数。

| 对象 |
|--------|
| 端口   |

 

此指示可在找到作为基于当前设置的关联的候选项时，由适配器发送。 接收到此指示后，主机会检查关联参数是否可用，如果是，则使用 [OID \_ WDI \_ 设置 \_ 关联 \_ 参数](oid-wdi-set-association-parameters.md)发送它们。

## <a name="payload-data"></a>负载数据


| 类型                                                                                                             | 允许多个 TLV 实例 | 可选 | 说明                                   |
|------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI \_ TLV \_ 关联 \_ 参数 \_ 请求的 \_ 类型**](./wdi-tlv-association-parameters-requested-type.md) |                                |          | 请求的关联参数的列表。 |
| [**WDI \_ TLV \_ BSS \_ 条目**](./wdi-tlv-bss-entry.md)                                                           | X                              | X        | BSSIDs 的列表。                           |

 

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 任务 \_ 连接](oid-wdi-task-connect.md)

 

