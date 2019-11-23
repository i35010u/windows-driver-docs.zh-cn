---
title: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY 为 TLV，其中包含 ASP2 播发服务项。
ms.assetid: CF7ED750-1987-4784-9E61-516EBBA22B9B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f62ba25ea795025f3bdda4345e008e76da3c5823
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840325"
---
# <a name="wdi_tlv_p2p_asp2_advertised_service_entry"></a>WDI\_TLV\_P2P\_ASP2\_公布\_SERVICE\_条目


WDI\_TLV\_P2P\_ASP2\_播发\_SERVICE\_项是包含 ASP2 播发服务项的 TLV。

**请注意**  此 TLV 添加到了 Windows 10 1607 版 WDI 版本1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12E

## <a name="length"></a>长度


所有包含的 TLVs 的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                           | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_服务\_类型**](wdi-tlv-p2p-service-type.md)               |                                |          | 服务的服务类型（UTF-8），最多21个字节。                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_服务\_类型\_哈希**](wdi-tlv-p2p-service-type-hash.md)    |                                |          | 服务类型的哈希。                                                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_实例\_名称**](wdi-tlv-p2p-instance-name.md)             |                                |          | 服务的实例类型（UTF-8），最大为63字节。                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_P2P\_实例\_名称\_哈希**](wdi-tlv-p2p-instance-name-hash.md)  |                                |          | "Instance Name，Service Type" 的哈希。                                                                                                                                                                                                                                                   |
| [**WDI\_TLV\_P2P\_服务\_信息**](wdi-tlv-p2p-service-information.md) |                                | X        | 服务的服务信息。                                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_服务\_状态**](wdi-tlv-p2p-service-status.md)           |                                |          | 服务的服务状态。                                                                                                                                                                                                                                                           |
| [**WDI\_TLV\_P2P\_播发\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | 唯一标识服务实例的 ID。                                                                                                                                                                                                                                     |
| [**WDI\_TLV\_P2P\_CONFIG\_方法**](wdi-tlv-p2p-config-methods.md)           |                                |          | WDI 中定义的配置方法[ **\_WPS\_配置\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)。 仅**WDI\_WPS\_配置\_方法\_显示**、 **WDI\_wps\_** \_\_\_\_\_\_\_ |

 

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

 

 




