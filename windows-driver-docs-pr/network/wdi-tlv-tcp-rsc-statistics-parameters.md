---
title: WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS
description: WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS 是包含 OID_WDI_TCP_RSC_STATISTICS 的 TCP RSC 统计信息的 TLV。
ms.assetid: C1459DF6-6492-4C1F-A22D-2BDC6492B29C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TCP_RSC_STATISTICS_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fbd8caf8d9ff8605e820fa53bd0365aac6b67827
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214987"
---
# <a name="wdi_tlv_tcp_rsc_statistics_parameters"></a>WDI \_ TLV \_ TCP \_ RSC \_ STATISTICS \_ 参数


WDI \_ tlv \_ tcp \_ rsc \_ STATISTICS \_ 参数是一个 tlv，其中包含 [OID \_ WDI \_ tcp \_ rsc \_ 统计信息](./oid-wdi-tcp-rsc-statistics.md)的 tcp RSC 统计信息。

## <a name="tlv-type"></a>TLV 类型


0xF3

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 说明                                                                                                                                                                                                                               |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT64 | 合并的数据包总数。                                                                                                                                                                                          |
| UINT64 | 合并的总字节数。                                                                                                                                                                                            |
| UINT64 | 合并事件总数，即通过合并数据包而形成的数据包总数。                                                                                                                     |
| UINT64 | RSC abort 事件的总数，即超出了 IP 数据报长度的除外。 此计数应包括由于硬件资源不足而未合并数据包的情况。 |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

