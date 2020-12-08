---
title: WDI_TLV_PORT_ATTRIBUTES
description: WDI_TLV_PORT_ATTRIBUTES 是包含端口属性的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PORT_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 57daf2a817b0b1e541ae31b749473f6cce80ea26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834275"
---
# <a name="wdi_tlv_port_attributes"></a>WDI \_ TLV \_ 端口 \_ 属性


WDI \_ tlv \_ 端口 \_ 属性是包含端口属性的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x29

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 描述                                         |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

