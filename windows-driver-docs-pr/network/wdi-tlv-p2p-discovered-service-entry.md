---
title: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY
description: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY 是包含发现的服务条目的 TLV。
ms.assetid: B8D453FF-49CA-4106-97DA-008893760E92
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1723107597ab9127e073e4685357126be1103fd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840448"
---
# <a name="wdi_tlv_p2p_discovered_service_entry"></a>WDI\_TLV\_P2P\_发现\_服务\_条目


已发现的 WDI\_TLV\_P2P\_\_服务\_项是包含发现的服务项的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x112

## <a name="length"></a>长度


所有包含的 TLVs 的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                           | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                               |
|--------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_服务\_名称**](wdi-tlv-p2p-service-name.md)               |                                |          | 服务的名称，采用 UTF-8，最大为255字节。                                                                                                                       |
| [**WDI\_TLV\_P2P\_服务\_信息**](wdi-tlv-p2p-service-information.md) |                                | X        | 服务的服务信息。                                                                                                                                  |
| [**WDI\_TLV\_P2P\_服务\_状态**](wdi-tlv-p2p-service-status.md)           |                                |          | 服务的服务状态。                                                                                                                                        |
| [**WDI\_TLV\_P2P\_播发\_ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | 唯一标识服务实例的 ID。                                                                                                                      |
| [**WDI\_TLV\_P2P\_CONFIG\_方法**](wdi-tlv-p2p-config-methods.md)           |                                |          | WDI 中定义的配置方法[ **\_WPS\_配置\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)。 只有 PinDisplay、PinKeypad 和 WFDS 适用。 |

 

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

 

 




