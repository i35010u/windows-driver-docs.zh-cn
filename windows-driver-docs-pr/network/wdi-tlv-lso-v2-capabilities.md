---
title: WDI_TLV_LSO_V2_CAPABILITIES
description: WDI_TLV_LSO_V2_CAPABILITIES 是包含大量发送卸载 V2 功能 TLV。
ms.assetid: 6F7C83BA-B004-431F-90AF-AD7DE1B13546
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LSO_V2_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4d9aae61f669f84c60f44efa0301ddb4d939fcc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543792"
---
# <a name="wditlvlsov2capabilities"></a>WDI\_TLV\_LSO\_V2\_功能


WDI\_TLV\_LSO\_V2\_功能是包含大量发送卸载 V2 功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0xCD

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                   | 允许多个 TLV 实例 | 可选 | 描述                                  |
|--------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI\_TLV\_IPV4\_LSO\_V2**](wdi-tlv-ipv4-lso-v2.md) |                                |          | IPv4 大型发送卸载 V2 的功能。 |
| [**WDI\_TLV\_IPV6\_LSO\_V2**](wdi-tlv-ipv6-lso-v2.md) |                                |          | IPv6 大型发送卸载 V2 的功能。 |

 

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

 

 




