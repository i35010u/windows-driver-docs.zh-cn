---
title: WDI_TLV_VIRTUALIZATION_CAPABILITIES
description: WDI_TLV_VIRTUALIZATION_CAPABILITIES 是包含虚拟化功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_VIRTUALIZATION_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6fa2d53a91b6537fb3c29eccd2d0509343b5c49b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834117"
---
# <a name="wdi_tlv_virtualization_capabilities"></a>WDI \_ TLV \_ 虚拟化 \_ 功能


WDI \_ tlv \_ 虚拟化 \_ 功能是包含虚拟化功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x10

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型  | 描述                                                                                                                                                                                                                       |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 受支持的 ExtSTA 端口数。                                                                                                                                                                                             |
| UINT8 | 支持 Wi-Fi 直接组端口的数量。 此计数只包含角色端口。 如果此值为非零值，则假定 Wi-Fi 的直接设备端口可用。                                               |
| UINT8 | 受支持的旧 ExtAP 端口的数量。                                                                                                                                                                                       |
| UINT8 | 同时支持的 AP/WFD 组所有者的最大数目。                                                                                                                                                                 |
| UINT8 | 设备可在其中运行并同时维护数据连接的单独通道的最大数量。 此限制不应包含临时多通道操作，如扫描和 Wi-Fi 直接协商。 |
| UINT8 | 受支持的同时 STA/WFD 客户端的最大数目。                                                                                                                                                                     |

 

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

 

 




