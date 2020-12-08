---
title: WDI_TLV_P2P_SERVICE_INFORMATION
description: WDI_TLV_P2P_SERVICE_INFORMATION 是包含 Wi-Fi 直接服务信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SERVICE_INFORMATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 59c38f639dce25eaf0fe7e70b3ef77bf13eb7399
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818785"
---
# <a name="wdi_tlv_p2p_service_information"></a>WDI \_ TLV \_ P2P \_ 服务 \_ 信息


WDI \_ tlv \_ P2P \_ 服务 \_ 信息是一个 tlv，其中包含 Wi-Fi 直接服务信息。

## <a name="tlv-type"></a>TLV 类型


0xEE

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                              |
|-----------|------------------------------------------|
| UINT8\[\] | 服务的服务信息。 |

 

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

 

 




