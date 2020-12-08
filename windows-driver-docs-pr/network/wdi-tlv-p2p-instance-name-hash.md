---
title: WDI_TLV_P2P_INSTANCE_NAME_HASH
description: WDI_TLV_P2P_INSTANCE_NAME_HASH 是包含 "Instance Name，Service Type" 的哈希值的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INSTANCE_NAME_HASH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bf0d3655d93f440373aa57cebc1da8b36f84221e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818245"
---
# <a name="wdi_tlv_p2p_instance_name_hash"></a>WDI \_ TLV \_ P2P \_ 实例 \_ 名称 \_ 哈希


WDI \_ tlv \_ P2P \_ 实例 \_ 名称 \_ 哈希是包含 "INSTANCE NAME，Service Type" 的哈希值的 tlv。

**注意**  此 TLV 已添加到 Windows 10 版本1607，WDI 版本1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x12C

## <a name="length"></a>长度


[**WDI \_ P2P \_ 服务 \_ 名称 \_ 哈希**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                                                    | 描述                                |
|-------------------------------------------------------------------------|--------------------------------------------|
| [**WDI \_ P2P \_ 服务 \_ 名称 \_ 哈希**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_p2p_service_name_hash) | "Instance Name，Service Type" 的哈希。 |

 

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

 

