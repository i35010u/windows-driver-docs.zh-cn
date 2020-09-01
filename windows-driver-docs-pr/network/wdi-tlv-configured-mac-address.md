---
title: WDI_TLV_CONFIGURED_MAC_ADDRESS
description: WDI_TLV_CONFIGURED_MAC_ADDRESS 是包含自定义 MAC 地址的 TLV。
ms.assetid: 2AB4AFF3-70E9-4E4B-885D-2578A5810A38
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONFIGURED_MAC_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fbdb4b9dc2b6b7f2603f4806860a48e0a87a0bd8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213720"
---
# <a name="wdi_tlv_configured_mac_address"></a>WDI \_ TLV \_ 配置的 \_ MAC \_ 地址


WDI \_ tlv \_ 配置的 \_ mac \_ 地址是包含自定义 mac 地址的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x99

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                              | 说明                                       |
|---------------------------------------------------|---------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 端口应使用的 MAC 地址。 |

 

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

 

