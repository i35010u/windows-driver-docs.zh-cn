---
title: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST
description: WDI_TLV_P2P_INTERFACE_ADDRESS_LIST 是一个 TLV，其中包含 Wi-fi Direct 接口的地址列表。
ms.assetid: B7FCB047-28D2-43E2-B4D6-B24E7BC74D47
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INTERFACE_ADDRESS_LIST 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 37ce045777c0bf70a2b40d8f463a7c5f9b223f2e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842758"
---
# <a name="wdi_tlv_p2p_interface_address_list"></a>WDI\_TLV\_P2P\_接口\_地址\_列表


WDI\_TLV\_P2P\_接口\_地址\_列表是一个 TLV，其中包含 Wi-fi Direct 接口的地址列表。

## <a name="tlv-type"></a>TLV 类型


0x18

## <a name="length"></a>长度


WDI 数组的大小（以字节为单位） [ **\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构。 数组必须包含1个或多个结构。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                  | 描述                      |
|-------------------------------------------------------|----------------------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | Wi-fi MAC 地址的数组。 |

 

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

 

 




