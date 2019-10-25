---
title: WDI_TLV_DISCONNECT_PARAMETERS
description: WDI_TLV_DISCONNECT_PARAMETERS 是一个 TLV，其中包含 OID_WDI_TASK_DISCONNECT 的参数。
ms.assetid: D0FF83A0-CD3B-47A6-BB08-842927F1D3BC
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISCONNECT_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bfd0a2435a3e26708cf95c62efeea279f04a8e3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834128"
---
# <a name="wdi_tlv_disconnect_parameters"></a>WDI\_TLV\_断开\_参数的连接


WDI\_TLV\_断开\_参数是一个 TLV，其中包含 OID 的参数[\_WDI\_任务\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-disconnect)。

## <a name="tlv-type"></a>TLV 类型


0x36

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                         |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 要解除关联的对等节点的 MAC 地址。                                                                                                                                        |
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
<td><p>Windows 10</p></td>
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

 

 




