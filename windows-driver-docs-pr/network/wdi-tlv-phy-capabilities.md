---
title: WDI_TLV_PHY_CAPABILITIES
description: WDI_TLV_PHY_CAPABILITIES 是包含 PHY 功能的 TLV。
ms.assetid: 8F482ED6-6594-4DB5-B53B-4424DAD32D36
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_CAPABILITIES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e57cf918a4916f08d497b43de94daa7d83f0570d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838018"
---
# <a name="wdi_tlv_phy_capabilities"></a>WDI\_TLV\_PHY\_功能


WDI\_TLV\_PHY\_功能是包含 PHY 功能的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x1B

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                        | 描述                                        |
|---------------------------------------------|----------------------------------------------------|
| [**WDI\_PHY\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type) | 指定 PHY 类型。                           |
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

 

 




