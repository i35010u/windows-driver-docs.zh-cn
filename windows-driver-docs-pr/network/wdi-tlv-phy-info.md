---
title: WDI_TLV_PHY_INFO
description: WDI_TLV_PHY_INFO 是包含 PHY 信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0b88d065a3698a17573b26c0fd39fdc8ad3faa33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818093"
---
# <a name="wdi_tlv_phy_info"></a>WDI \_ TLV \_ PHY \_ 信息


WDI \_ tlv \_ PHY \_ 信息是包含 PHY 信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x26

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                             | 允许多个 TLV 实例 | 可选 | 说明                |
|----------------------------------------------------------------------------------|--------------------------------|----------|----------------------------|
| [**WDI \_ TLV \_ PHY \_ 功能**](wdi-tlv-phy-capabilities.md)                  |                                |          | Phy 功能。      |
| [**WDI \_ TLV \_ PHY \_ TX \_ 电源 \_ 级别 \_ 列表**](wdi-tlv-phy-tx-power-level-list.md) |                                |          | TX 电源级别的列表。 |
| [**WDI \_ TLV \_ PHY \_ 数据 \_ 速率 \_ 列表**](wdi-tlv-phy-data-rate-list.md)            |                                |          | 数据速率列表。      |

 

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

 

 




