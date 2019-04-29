---
title: WDI_TLV_DISCONNECT_PARAMETERS
description: WDI_TLV_DISCONNECT_PARAMETERS 是包含参数的 OID_WDI_TASK_DISCONNECT TLV。
ms.assetid: D0FF83A0-CD3B-47A6-BB08-842927F1D3BC
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DISCONNECT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d7c1fb88e0f9796207ff57ec23ff096ae1c1fdd1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380875"
---
# <a name="wditlvdisconnectparameters"></a>WDI\_TLV\_断开连接\_参数


WDI\_TLV\_断开连接\_参数是包含参数的 TLV [OID\_WDI\_任务\_断开连接](https://msdn.microsoft.com/library/windows/hardware/dn925951)。

## <a name="tlv-type"></a>TLV 类型


0x36

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                         |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 若要解除关联的对等方 MAC 地址。                                                                                                                                        |
| UINT16                                            | 主机触发解除关联的原因。 此值在 little-endian 字节顺序中提供，并且应适当地复制到传出的帧，原因代码。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




