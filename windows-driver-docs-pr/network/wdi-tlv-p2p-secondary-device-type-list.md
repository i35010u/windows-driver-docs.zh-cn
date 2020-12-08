---
title: WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST
description: WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST 是包含一系列辅助设备类型的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4051efc214c7a075d7c0cc1933ff9fc7c503f65c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818171"
---
# <a name="wdi_tlv_p2p_secondary_device_type_list"></a>WDI \_ TLV \_ P2P \_ 辅助 \_ 设备 \_ 类型 \_ 列表


WDI \_ tlv \_ P2P \_ 辅助 \_ 设备 \_ 类型 \_ 列表是包含一系列辅助设备类型的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x94

## <a name="length"></a>长度


WDI \_ P2P \_ 设备类型元素数组的大小 (以字节为单位) \_ 。 允许数组长度为0。

**注意**  WDI \_ P2P \_ 设备 \_ 类型不是 WDI 结构。 它在 WDI TLV 分析程序生成器中定义，仅用于文档目的。

 

## <a name="values"></a>值


| 类型                       | 描述                            |
|----------------------------|----------------------------------------|
| WDI \_ P2P \_ 设备 \_ 类型\[\] | Wi-Fi 直接设备类型的数组。 |

 

WDI \_ P2P \_ 设备 \_ 类型由以下元素组成。

| 类型       | 描述                                   |
|------------|-----------------------------------------------|
| UINT16     | 主类型类别 ID。                    |
| UINT8 \[ 4\] | 分配给此设备类型的 OUI。 |
| UINT16     | 子类别 ID。                           |

 

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

 

 




