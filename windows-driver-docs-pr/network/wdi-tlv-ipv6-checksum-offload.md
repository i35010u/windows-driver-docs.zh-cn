---
title: WDI_TLV_IPV6_CHECKSUM_OFFLOAD
description: WDI_TLV_IPV6_CHECKSUM_OFFLOAD 是 IPv6 的包含校验和卸载功能 TLV。
ms.assetid: 878471F5-8118-4D0A-87BC-E44DE7A713DF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IPV6_CHECKSUM_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7297b677ce816088fdc78e4679b366e4ff5465b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524440"
---
# <a name="wditlvipv6checksumoffload"></a>WDI\_TLV\_IPV6\_CHECKSUM\_OFFLOAD


WDI\_TLV\_IPV6\_校验和\_卸载是 IPv6 的包含校验和卸载功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0xD0

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                  |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI\_TLV\_CHECKSUM\_OFFLOAD\_V6\_TX\_PARAMETERS**](wdi-tlv-checksum-offload-v6-tx-parameters.md) |                                |          | IPv6 的卸载参数的 Tx 校验和。 |
| [**WDI\_TLV\_CHECKSUM\_OFFLOAD\_V6\_RX\_PARAMETERS**](wdi-tlv-checksum-offload-v6-rx-parameters.md) |                                |          | IPv6 的卸载参数的 Rx 校验和。 |

 

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

 

 




