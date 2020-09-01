---
title: WDI_TLV_PHY_CAPABILITIES
description: WDI_TLV_PHY_CAPABILITIES 是包含 PHY 功能的 TLV。
ms.assetid: 8F482ED6-6594-4DB5-B53B-4424DAD32D36
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d3a58cbc1b60e7c0f125150d8ebdd00ffdc10318
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213728"
---
# <a name="wdi_tlv_phy_capabilities"></a>WDI \_ TLV \_ PHY \_ 功能


WDI \_ tlv \_ PHY \_ 功能是包含 PHY 功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x1B

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                        | 说明                                        |
|---------------------------------------------|----------------------------------------------------|
| [**WDI \_ PHY \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type) | 指定 PHY 类型。                           |
| UINT8                                       | 指定 PHY 是否支持 CF 轮询。 |
| UINT32                                      | 指定 MPDU 的最大长度。                 |
| UINT32                                      | 指定操作温度类。         |
| UINT32                                      | 指定天线多样性支持。           |

 

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

 

