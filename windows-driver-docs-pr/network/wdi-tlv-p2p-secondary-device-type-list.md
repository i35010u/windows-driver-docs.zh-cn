---
title: WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST
description: WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST 是 TLV 包含辅助设备类型的列表。
ms.assetid: 278F3D2B-6729-4F7A-B3B2-B12D79C04530
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c0c9d4317a159c6e413ef6b6097dafcf5232690b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565358"
---
# <a name="wditlvp2psecondarydevicetypelist"></a>WDI\_TLV\_P2P\_辅助\_设备\_类型\_列表


WDI\_TLV\_P2P\_辅助\_设备\_类型\_列表是包含一系列辅助设备类型 TLV。

## <a name="tlv-type"></a>TLV 类型


0x94

## <a name="length"></a>长度


WDI 的数组的大小 （以字节为单位）\_P2P\_设备\_类型元素。 允许数组长度为 0。

**请注意**  WDI\_P2P\_设备\_类型不是 WDI 结构。 它定义在 WDI TLV 分析器生成器，并仅供文档使用。

 

## <a name="values"></a>值


| 在任务栏的搜索框中键入                       | 描述                            |
|----------------------------|----------------------------------------|
| WDI\_P2P\_DEVICE\_TYPE\[\] | Wi-Fi Direct 设备类型的数组。 |

 

WDI\_P2P\_设备\_类型由以下元素组成。

| 在任务栏的搜索框中键入       | 描述                                   |
|------------|-----------------------------------------------|
| UINT16     | 主要类型类别 id。                    |
| UINT8\[4\] | 分配给此设备类型 OUI。 |
| UINT16     | 子类别 id。                           |

 

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

 

 




