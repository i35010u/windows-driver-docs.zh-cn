---
title: WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR
description: WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR 是包含 Wi-Fi 直接服务更新指示器的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_UPDATE_INDICATOR 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 49a613d4c7c13a39b33029d4b22dc2d9e6089af0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818121"
---
# <a name="wdi_tlv_p2p_service_update_indicator"></a>WDI \_ TLV \_ P2P \_ 服务 \_ 更新 \_ 指示器


WDI \_ tlv \_ P2P \_ 服务 \_ 更新 \_ 指示器是包含 Wi-Fi 直接服务更新指示器的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x115

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                                 |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16 | 如果驱动程序支持响应服务信息发现 ANQP 请求，则包含在 ANQP 响应中的服务更新指示器。 |

 

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

 

 




