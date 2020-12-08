---
title: WDI_TLV_P2P_ACTION_FRAME_IES
description: WDI_TLV_P2P_ACTION_FRAME_IES 是包含操作帧的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ACTION_FRAME_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 24972b1fa5c9c08d2552998a7236d49f977f5285
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787163"
---
# <a name="wdi_tlv_p2p_action_frame_ies"></a>WDI \_ TLV \_ P2P \_ 操作 \_ 帧 \_


WDI \_ tlv \_ P2P \_ 操作 \_ 帧 \_ 是包含操作帧的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x90

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素的数组，这些元素指定发送到远程设备的一组内容。 |

 

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

 

 




