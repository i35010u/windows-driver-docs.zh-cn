---
title: WDI_TLV_MULTICAST_LIST
description: WDI_TLV_MULTICAST_LIST 是 TLV 包含多播 MAC 地址的数组。
ms.assetid: 5023557A-1BC5-4A4E-A77C-20353C0CA3FD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_MULTICAST_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bd87e58f2f4208ca0f13071a426ee618fa06d0b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386952"
---
# <a name="wditlvmulticastlist"></a>WDI\_TLV\_MULTICAST\_LIST


WDI\_TLV\_多播\_列表是 TLV 包含多播 MAC 地址的数组。

## <a name="tlv-type"></a>TLV 类型


0x6A

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构。 该数组必须包含一个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                  | 描述                          |
|-------------------------------------------------------|--------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | 数组的多播 MAC 地址。 |

 

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

 

 




