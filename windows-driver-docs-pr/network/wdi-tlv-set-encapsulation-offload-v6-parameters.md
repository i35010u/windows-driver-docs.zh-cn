---
title: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS
description: WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS 是一个 TLV，由 OID_WDI_SET_ENCAPSULATION_OFFLOAD 用来指示 IPv6 卸载是否应启动。
ms.assetid: 7036AFD0-197E-4A94-8580-A42889BE6798
ms.date: 07/18/2017
keywords:
- WDI_TLV_SET_ENCAPSULATION_OFFLOAD_V6_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c67b4357335b618be82db93f64f9ff903ac6baca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841727"
---
# <a name="wdi_tlv_set_encapsulation_offload_v6_parameters"></a>WDI\_TLV\_设置\_封装\_卸载\_V6\_参数


WDI\_TLV\_设置\_封装\_卸载\_V6\_参数是 OID 使用的 TLV\_[WDI\_设置\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-encapsulation-offload)\_将启动。

## <a name="tlv-type"></a>TLV 类型


0xFE

## <a name="length"></a>长度


UINT8 的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                                                             |
|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 指定是否应启动 IPv6 卸载。 如果启用，此值设置为 NDIS\_卸载\_将\_设置为 "启用"，并将设置为 "NDIS\_卸载"\_禁用 "禁用"。 |

 

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

## <a name="see-also"></a>另请参阅


[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

 

 




