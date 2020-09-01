---
title: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY
description: WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY 是包含发现的服务项的 TLV。
ms.assetid: B8D453FF-49CA-4106-97DA-008893760E92
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DISCOVERED_SERVICE_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 86c6c39efb9cf5a2754cda2cd432c72b78366ca0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211511"
---
# <a name="wdi_tlv_p2p_discovered_service_entry"></a>WDI \_ TLV \_ P2P \_ 发现的 \_ 服务 \_ 条目


WDI \_ tlv \_ P2P \_ 发现的 \_ 服务 \_ 条目是包含发现的服务条目的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x112

## <a name="length"></a>Length


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                           | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                               |
|--------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 名称**](wdi-tlv-p2p-service-name.md)               |                                |          | 服务的名称，采用 UTF-8，最大为255字节。                                                                                                                       |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 信息**](wdi-tlv-p2p-service-information.md) |                                | X        | 服务的服务信息。                                                                                                                                  |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 状态**](wdi-tlv-p2p-service-status.md)           |                                |          | 服务的服务状态。                                                                                                                                        |
| [**WDI \_ TLV \_ P2P \_ 播发 \_ ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | 唯一标识服务实例的 ID。                                                                                                                      |
| [**WDI \_ TLV \_ P2P \_ CONFIG \_ 方法**](wdi-tlv-p2p-config-methods.md)           |                                |          | [**WDI \_ WPS \_ 配置 \_ 方法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)中定义的配置方法。 只有 PinDisplay、PinKeypad 和 WFDS 适用。 |

 

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

 

