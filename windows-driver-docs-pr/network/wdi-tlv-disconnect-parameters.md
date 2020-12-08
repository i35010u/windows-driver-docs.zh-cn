---
title: WDI_TLV_DISCONNECT_PARAMETERS
description: WDI_TLV_DISCONNECT_PARAMETERS 是包含 OID_WDI_TASK_DISCONNECT 的参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISCONNECT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4be6ec174d7bc1895bb98495b902c481a05faffe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803473"
---
# <a name="wdi_tlv_disconnect_parameters"></a>WDI \_ TLV \_ 断开 \_ 参数


WDI \_ tlv \_ disconnect \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ TASK \_ disconnect](./oid-wdi-task-disconnect.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0x36

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 描述                                                                                                                                                                         |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

