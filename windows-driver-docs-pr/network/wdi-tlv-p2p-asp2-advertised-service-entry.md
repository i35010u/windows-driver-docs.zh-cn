---
title: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY
description: WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY 为 TLV，其中包含 ASP2 播发服务项。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 436b6e6747a53471e846abb7c4666257bf593075
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823777"
---
# <a name="wdi_tlv_p2p_asp2_advertised_service_entry"></a>WDI \_ TLV \_ P2P \_ ASP2 \_ 播发 \_ 服务 \_ 条目


WDI \_ TLV \_ P2P \_ ASP2 \_ 播发 \_ 服务 \_ 项是包含 ASP2 播发服务项的 tlv。

**注意**  此 TLV 已添加到 Windows 10 版本1607，WDI 版本1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12E

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                           | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 类型**](wdi-tlv-p2p-service-type.md)               |                                |          | 服务的服务类型 (UTF-8) ，最多21个字节。                                                                                                                                                                                                                                     |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 类型 \_ 哈希**](wdi-tlv-p2p-service-type-hash.md)    |                                |          | 服务类型的哈希。                                                                                                                                                                                                                                                                    |
| [**WDI \_ TLV \_ P2P \_ 实例 \_ 名称**](wdi-tlv-p2p-instance-name.md)             |                                |          | 服务的实例类型 (UTF-8) ，最大为63字节。                                                                                                                                                                                                                                    |
| [**WDI \_ TLV \_ P2P \_ 实例 \_ 名称 \_ 哈希**](wdi-tlv-p2p-instance-name-hash.md)  |                                |          | "Instance Name，Service Type" 的哈希。                                                                                                                                                                                                                                                   |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 信息**](wdi-tlv-p2p-service-information.md) |                                | X        | 服务的服务信息。                                                                                                                                                                                                                                                     |
| [**WDI \_ TLV \_ P2P \_ 服务 \_ 状态**](wdi-tlv-p2p-service-status.md)           |                                |          | 服务的服务状态。                                                                                                                                                                                                                                                           |
| [**WDI \_ TLV \_ P2P \_ 播发 \_ ID**](wdi-tlv-p2p-advertisement-id.md)       |                                |          | 唯一标识服务实例的 ID。                                                                                                                                                                                                                                     |
| [**WDI \_ TLV \_ P2P \_ CONFIG \_ 方法**](wdi-tlv-p2p-config-methods.md)           |                                |          | [**WDI \_ WPS \_ 配置 \_ 方法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_wps_configuration_method)中定义的配置方法。 只有 **WDI \_ wps \_ 配置 \_ 方法 \_ 显示**、 **WDI \_ wps \_ 配置 \_ 方法 \_ 键盘** 和 **WDI \_ WPS 配置 \_ 方法 \_ \_ WFDS \_ 默认值** 适用。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

