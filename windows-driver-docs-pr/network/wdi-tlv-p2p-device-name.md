---
title: WDI_TLV_P2P_DEVICE_NAME
description: WDI_TLV_P2P_DEVICE_NAME 是包含设备名称的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_NAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d72969f3afaf6c087bb11af470220214bf1c30ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823707"
---
# <a name="wdi_tlv_p2p_device_name"></a>WDI \_ TLV \_ P2P \_ 设备 \_ 名称


WDI \_ tlv \_ P2P \_ DEVICE \_ name 是包含设备名称的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x92

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                               |
|-----------|---------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素的数组，用于指定设备的设备名称。 |

 

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

 

 




