---
title: WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES
description: WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES 是 TLV 包含 IPv4 和 IPv6 的校验和卸载功能。
ms.assetid: 400D532F-CAAA-40F9-8001-EE460D4C89F9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHECKSUM_OFFLOAD_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7bcfede0805a8f792eb7aabc6210e928be3e619d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329817"
---
# <a name="wditlvchecksumoffloadcapabilities"></a>WDI\_TLV\_CHECKSUM\_卸载\_功能


WDI\_TLV\_CHECKSUM\_卸载\_功能是包含 IPv4 和 IPv6 的校验和卸载功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0xCB

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                       | 允许多个 TLV 实例 | 可选 | 描述                           |
|----------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------|
| [**WDI\_TLV\_IPV4\_CHECKSUM\_OFFLOAD**](wdi-tlv-ipv4-checksum-offload.md) |                                |          | 参数的 IPv4 校验和卸载。 |
| [**WDI\_TLV\_IPV6\_CHECKSUM\_OFFLOAD**](wdi-tlv-ipv6-checksum-offload.md) |                                |          | 参数的 IPv6 校验和卸载。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




