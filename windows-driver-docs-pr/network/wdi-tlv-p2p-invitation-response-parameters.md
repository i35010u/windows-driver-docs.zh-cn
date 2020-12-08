---
title: WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS 是包含 Wi-Fi 直接邀请响应参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INVITATION_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5a28d89bc58fe374c0ca5bac66cfb9eb4a81fe3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818229"
---
# <a name="wdi_tlv_p2p_invitation_response_parameters"></a>WDI \_ TLV \_ P2P \_ 邀请 \_ 响应 \_ 参数


WDI \_ tlv \_ P2P \_ 邀请 \_ 响应 \_ 参数是包含 Wi-Fi 直接邀请响应参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x80

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型   | 描述                                                                    |
|--------|--------------------------------------------------------------------------------|
| UINT8  | Wi-Fi 直接状态代码，如 Wi-Fi 直接规范指定的一样。 |
| UINT16 | 中转配置超时（以毫秒为单位）。                                 |
| UINT16 | 客户端配置超时（以毫秒为单位）。                             |

 

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

 

 




