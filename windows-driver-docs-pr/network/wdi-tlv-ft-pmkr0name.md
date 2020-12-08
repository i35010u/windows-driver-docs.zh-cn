---
title: WDI_TLV_FT_PMKR0NAME
description: WDI_TLV_FT_PMKR0NAME 是一种 TLV，其中包含 PMKR0Name 或 PMKR1Name (802.11 r) 。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_PMKR0NAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0181475d36c940791ef646883346448408e95172
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801249"
---
# <a name="wdi_tlv_ft_pmkr0name"></a>WDI \_ TLV \_ FT \_ PMKR0NAME


WDI \_ tlv \_ FT \_ PMKR0NAME 是一种 tlv，其中包含 PMKR0NAME 或 PMKR1Name (802.11 r) 。

## <a name="tlv-type"></a>TLV 类型


0x107

## <a name="length"></a>长度


[**WDI \_ 类型 \_ PMK \_ 名称**](/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_type_pmk_name)结构的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型                                                   | 描述                         |
|--------------------------------------------------------|-------------------------------------|
| [**WDI \_ 类型 \_ PMK \_ 名称**](/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_type_pmk_name) |  (802.11 r) 的 PMKR0Name 或 PMKR1Name。 |

 

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

 

