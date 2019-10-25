---
title: WDI_TLV_MULTICAST_LIST
description: WDI_TLV_MULTICAST_LIST 是一个 TLV，其中包含多播 MAC 地址的数组。
ms.assetid: 5023557A-1BC5-4A4E-A77C-20353C0CA3FD
ms.date: 07/18/2017
keywords:
- WDI_TLV_MULTICAST_LIST 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9e634598f6e530ec85582a8f2a7457e58d1b1697
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844981"
---
# <a name="wdi_tlv_multicast_list"></a>WDI\_TLV\_多播\_列表


WDI\_TLV\_多播\_列表是包含多播 MAC 地址数组的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x6A

## <a name="length"></a>长度


WDI 数组的大小（以字节为单位） [ **\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                  | 描述                          |
|-------------------------------------------------------|--------------------------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | 多播 MAC 地址的数组。 |

 

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

 

 




