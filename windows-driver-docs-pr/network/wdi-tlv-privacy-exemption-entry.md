---
title: WDI_TLV_PRIVACY_EXEMPTION_ENTRY
description: WDI_TLV_PRIVACY_EXEMPTION_ENTRY 是包含隐私例外项的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PRIVACY_EXEMPTION_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: daf4e5dddda5270b11c39093a370856d6aa197d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818035"
---
# <a name="wdi_tlv_privacy_exemption_entry"></a>WDI \_ TLV \_ 隐私 \_ 豁免 \_ 条目


WDI \_ tlv \_ 隐私 \_ 例外 \_ 项是包含隐私例外项的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x48

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                   | 描述                                                 |
|------------------------------------------------------------------------|-------------------------------------------------------------|
| UINT16                                                                 | 以大字节序字节顺序指定 IEEE EtherType。      |
| [**WDI \_ 豁免 \_ 操作 \_ 类型**](/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_exemption_action_type) | 指定例外的操作类型。                 |
| [**WDI \_ 免除 \_ 数据包 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_exemption_packet_type) | 指定豁免适用的数据包类型。 |

 

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

 

