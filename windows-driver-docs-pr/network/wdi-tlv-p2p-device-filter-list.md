---
title: WDI_TLV_P2P_DEVICE_FILTER_LIST
description: WDI_TLV_P2P_DEVICE_FILTER_LIST 是包含一系列 Wi-Fi Direct 设备 TLV 和组所有者要在 Wi-Fi Direct 设备发现期间搜索。
ms.assetid: 56D1E6BD-41E3-4869-A821-334012B781A7
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_FILTER_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e90369d8c488671416b8808bc037b28764501f7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355106"
---
# <a name="wditlvp2pdevicefilterlist"></a>WDI\_TLV\_P2P\_DEVICE\_FILTER\_LIST


WDI\_TLV\_P2P\_设备\_筛选器\_列表是包含一系列 Wi-Fi Direct 设备 TLV 和组所有者要在 Wi-Fi Direct 设备发现期间搜索。

## <a name="tlv-type"></a>TLV 类型


0xCE

## <a name="length"></a>长度


数组的大小 （以字节为单位） [ **WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构。 该数组必须包含一个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                  | 描述                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | Wi-Fi Direct 设备和组所有者在 Wi-Fi Direct 设备发现期间搜索的列表。 |

 

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

 

 




