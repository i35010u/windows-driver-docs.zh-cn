---
title: WDI_TLV_P2P_DEVICE_FILTER_LIST
description: WDI_TLV_P2P_DEVICE_FILTER_LIST 是一种 TLV，其中包含 wi-fi direct 设备的列表和在 Wi-fi Direct 设备发现期间要搜索的组所有者。
ms.assetid: 56D1E6BD-41E3-4869-A821-334012B781A7
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_DEVICE_FILTER_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ed26db388021d47d89bd7d558b8fdf274cc80cec
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208487"
---
# <a name="wdi_tlv_p2p_device_filter_list"></a>WDI \_ TLV \_ P2P \_ 设备 \_ 筛选器 \_ 列表


WDI \_ tlv \_ P2P \_ DEVICE \_ FILTER \_ LIST 是一个 tlv，其中包含 wi-fi direct 设备的列表和在 wi-fi direct 设备发现期间要搜索的组所有者。

## <a name="tlv-type"></a>TLV 类型


0xCE

## <a name="length"></a>Length


[**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构数组的大小 (以字节为单位) 。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 类型                                                  | 说明                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | 在 Wi-fi Direct 设备发现期间要搜索的 Wi-fi Direct 设备和组所有者列表。 |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

