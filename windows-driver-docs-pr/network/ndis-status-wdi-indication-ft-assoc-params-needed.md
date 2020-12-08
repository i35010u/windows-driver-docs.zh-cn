---
title: NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED 来请求 802.11 r 漫游的参数。ObjectPort .
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_FT_ASSOC_PARAMS_NEEDED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c4224d277d14b5f9741ccbcd3dc74eabbc240e6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801393"
---
# <a name="ndis_status_wdi_indication_ft_assoc_params_needed"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ \_ 需要 FT ASSOC \_ 参数 \_


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ FT \_ ASSOC 参数 \_ \_ 来请求 802.11 r 漫游的参数。

| 对象 |
|--------|
| 端口   |

 

在 [OID \_ WDI \_ 任务 \_ 漫游](oid-wdi-task-roam.md)期间，WDI 提供用于将 802.11 Authentication 请求发送 (PmkR0Name，R0KH-ID，SNonce，MDIE) 的参数。 接收到身份验证响应后，LE 请求重新关联请求所需的其他参数，例如 PMKR1Name 和 R1KH。 该 LE 还会将身份验证响应中收到的参数发送 (ANonce、SNonce 和 R1KHID) 。

对于初始移动域成功完成的连接，该 LE 只应 (Fast 漫游) 中执行11r 漫游。 该 LE 可以使用操作系统提供的候选列表，或将其自己用于漫游。 如果该 LE 使用其自己的候选列表，则必须使用操作系统建议的任何一个候选项中提供的参数 (MDE、FTE 和 PMKR0Name) ，才能执行11r 漫游。 只要连接处于 FIPS 模式，11r 就会被禁用。 11r 快速漫游目前仅支持 FT over 1x 身份验证类型。

## <a name="payload-data"></a>负载数据


| 类型                                                                  | 允许多个 TLV 实例 | 可选 | 说明                            |
|-----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI \_ TLV \_ BSSID**](./wdi-tlv-bssid.md)                         |                                |          | AP 的 BSSID。                   |
| [**WDI \_ TLV \_ FT \_ 身份验证 \_ 请求**](./wdi-tlv-ft-auth-request.md)   |                                |          | 身份验证请求字节 blob。  |
| [**WDI \_ TLV \_ FT \_ 身份验证 \_ 响应**](./wdi-tlv-ft-auth-response.md) |                                |          | 身份验证响应字节 blob。 |

 

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


[OID \_ WDI \_ 任务 \_ 漫游](oid-wdi-task-roam.md)

 

