---
title: WDI_TLV_BSSID
description: WDI_TLV_BSSID 是包含 BSS BSSID 的 TLV。
ms.assetid: 0B3AB317-D1E7-4E61-9F6E-C3134B5A3984
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSSID 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e5da548315e36b9892e44f3870cd214721d5ed5d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844512"
---
# <a name="wdi_tlv_bssid"></a>WDI\_TLV\_BSSID


WDI\_TLV\_BSSID 是包含 BSS BSSID 的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x2

## <a name="length"></a>长度


[**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)结构的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                 |
|---------------------------------------------------|---------------------------------------------|
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 指定 BSSID 的 Wi-fi MAC 地址。 |

 

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

 

 




