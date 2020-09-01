---
title: WDI_TLV_CREATE_PORT_MAC_ADDRESS
description: WDI_TLV_CREATE_PORT_MAC_ADDRESS 是包含 OID_WDI_TASK_CREATE_PORT 的 MAC 地址的 TLV。
ms.assetid: CE2174E2-CFD7-40E7-B8A2-B96DDB6D6AA4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CREATE_PORT_MAC_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 205f6d09c941c011c416675d926850fa89121f35
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211519"
---
# <a name="wdi_tlv_create_port_mac_address"></a>WDI \_ TLV \_ 创建 \_ 端口 \_ MAC \_ 地址


WDI \_ tlv \_ CREATE \_ 端口 \_ MAC \_ 地址是一个 TLV，其中包含 [OID \_ WDI \_ TASK \_ CREATE \_ 端口](./oid-wdi-task-create-port.md)的 MAC 地址。

## <a name="tlv-type"></a>TLV 类型


0xD9

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                              | 说明                                   |
|---------------------------------------------------|-----------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 要用于端口创建的 MAC 地址。 |

 

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

 

