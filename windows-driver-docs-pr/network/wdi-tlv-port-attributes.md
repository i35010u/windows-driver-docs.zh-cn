---
title: WDI_TLV_PORT_ATTRIBUTES
description: WDI_TLV_PORT_ATTRIBUTES 是包含端口属性的 TLV。
ms.assetid: F5A0BC8D-1B86-41C2-A530-860E15775695
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PORT_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 88b8ef56a24d75275ec2e6a32cfbd73160f92054
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207151"
---
# <a name="wdi_tlv_port_attributes"></a>WDI \_ TLV \_ 端口 \_ 属性


WDI \_ tlv \_ 端口 \_ 属性是包含端口属性的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x29

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 说明                                         |
|---------------------------------------------------|-----------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定与端口关联的 MAC 地址。 |
| UINT16                                            | 指定端口号。                          |

 

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

 

