---
title: WDI_TLV_PACKET_FILTER_PARAMETERS
description: WDI_TLV_PACKET_FILTER_PARAMETERS 是一个 TLV，其中包含 OID_WDI_SET_RECEIVE_PACKET_FILTER 的数据包筛选器参数。
ms.assetid: 5B26DA60-BC5D-4CC5-A620-C076CECF22C0
ms.date: 07/18/2017
keywords:
- WDI_TLV_PACKET_FILTER_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ce40386c62c02bf00f302aaaeb14ac4e414fd86d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845152"
---
# <a name="wdi_tlv_packet_filter_parameters"></a>WDI\_TLV\_数据包\_筛选器\_参数


WDI\_TLV\_数据包\_筛选器\_参数是一个 TLV，其中包含 OID 的数据包筛选器参数\_\_\_\_\_[筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-receive-packet-filter)。

## <a name="tlv-type"></a>TLV 类型


0x47

## <a name="length"></a>长度


UINT32 的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                      | 描述                                |
|---------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_包\_筛选器\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_packet_filter_type)（UINT32） | 指定所需的 Wi-fi 数据包筛选器。 |

 

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
<td><p>Windows 10</p></td>
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

 

 




