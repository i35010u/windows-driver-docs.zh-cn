---
title: WDI_TLV_DISCONNECT_PARAMETERS
description: WDI_TLV_DISCONNECT_PARAMETERS 是包含 OID_WDI_TASK_DISCONNECT 的参数的 TLV。
ms.assetid: D0FF83A0-CD3B-47A6-BB08-842927F1D3BC
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISCONNECT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4c4e01a09ad5d33a526ba1e1a5e45ec03b982499
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214995"
---
# <a name="wdi_tlv_disconnect_parameters"></a>WDI \_ TLV \_ 断开 \_ 参数


WDI \_ tlv \_ disconnect \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ TASK \_ disconnect](./oid-wdi-task-disconnect.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0x36

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 说明                                                                                                                                                                         |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 要解除关联的对等节点的 MAC 地址。                                                                                                                                        |
| UINT16                                            | 主机触发解除进一步的原因。 此值以 little endian 字节顺序提供，并应适当地复制到传出帧的原因代码中。 |

 

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

 

