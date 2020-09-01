---
title: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY 是包含播发服务项的 TLV。
ms.assetid: C9BBA5D4-EC51-4D03-B997-A95B3168E64F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ADVERTISED_SERVICE_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7625f0689deb96e2e7367d01204ce8eb9287afb6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218294"
---
# <a name="wdi_tlv_p2p_advertised_service_entry"></a>WDI \_ TLV \_ P2P \_ 播发 \_ 服务 \_ 条目


WDI \_ tlv \_ P2P \_ 播发 \_ 服务 \_ 项是包含播发服务项的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xFC

## <a name="length"></a>Length


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                           | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 名称**](wdi-tlv-p2p-service-name.md)               |                                |          | 服务的名称，采用 UTF-8，最大为255字节。                                                                                                                          |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 名称 \_ 哈希**](wdi-tlv-p2p-service-name-hash.md)    |                                |          | 服务名称哈希。                                                                                                                                                    |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 信息**](wdi-tlv-p2p-service-information.md) |                                | X        | 此服务的服务信息。                                                                                                                                    |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 状态**](wdi-tlv-p2p-service-status.md)           |                                |          | 此服务的服务状态。                                                                                                                                          |
| [**WDI \_ TLV \_ P2P \_ 播发 \_ ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | 唯一标识服务实例的 ID。                                                                                                                     |
| [**WDI \_ TLV \_ P2P \_ CONFIG \_ 方法**](wdi-tlv-p2p-config-methods.md)           |                                |          | [**WDI \_ WPS \_ 配置 \_ 方法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)中定义的配置方法。 仅 PIN 显示、PIN 键盘和 WFDS 适用。 |

 

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

 

