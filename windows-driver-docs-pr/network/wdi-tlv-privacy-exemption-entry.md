---
title: WDI_TLV_PRIVACY_EXEMPTION_ENTRY
description: WDI_TLV_PRIVACY_EXEMPTION_ENTRY 是包含隐私例外项的 TLV。
ms.assetid: 086BD366-F54C-4BF4-8544-CC2AB2472EB2
ms.date: 07/18/2017
keywords:
- WDI_TLV_PRIVACY_EXEMPTION_ENTRY 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f733f6fffd3e397e7423a6854183f3942be70754
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844586"
---
# <a name="wdi_tlv_privacy_exemption_entry"></a>WDI\_TLV\_隐私\_豁免\_条目


WDI\_TLV\_隐私\_免除\_条目是包含隐私豁免条目的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x48

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                   | 描述                                                 |
|------------------------------------------------------------------------|-------------------------------------------------------------|
| UINT16                                                                 | 以大字节序字节顺序指定 IEEE EtherType。      |
| [**WDI\_豁免\_操作\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_exemption_action_type) | 指定例外的操作类型。                 |
| [**WDI\_豁免\_数据包\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_exemption_packet_type) | 指定豁免适用的数据包类型。 |

 

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

 

 




