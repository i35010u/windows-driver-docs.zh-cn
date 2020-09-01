---
title: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS
description: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS 是由 OID_WDI_SET_ENCAPSULATION_OFFLOAD 使用的 TLV，用于指示是否应启动 IPv6 卸载。
ms.assetid: 7036AFD0-197E-4A94-8580-A42889BE6798
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e1434186d50ce11acd9bd8c7c3afe3d89147552a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206161"
---
# <a name="wdi_tlv_set_encapsulation_offload_v6_parameters"></a>WDI \_ TLV \_ 设置 \_ 封装 \_ 卸载 \_ V6 \_ 参数


WDI \_ tlv \_ 集 \_ 封装 \_ 卸载 \_ V6 \_ 参数是由 [OID \_ WDI \_ 设置 \_ \_ ](./oid-wdi-set-encapsulation-offload.md) 的 tlv，用于指示是否应启动 IPv6 卸载。

## <a name="tlv-type"></a>TLV 类型


0xFE

## <a name="length"></a>Length


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型  | 说明                                                                                                                                             |
|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 指定是否应启动 IPv6 卸载。 如果启用了此值，则将此值设置为 \_ 启用 ndis 卸载 \_ 集 \_ ，并将设置为 " \_ 禁用后禁用 ndis 卸载" \_ \_ 。 |

 

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

## <a name="see-also"></a>另请参阅


[**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

 

