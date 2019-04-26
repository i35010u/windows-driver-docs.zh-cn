---
title: WDI_TLV_IPV4_CHECKSUM_OFFLOAD
description: WDI_TLV_IPV4_CHECKSUM_OFFLOAD 是包含校验和卸载功能的 IPv4 TLV。
ms.assetid: FCC5880E-4323-4A24-98C6-CE7C84D03C16
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IPV4_CHECKSUM_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 856197e294922427b34d1e28f4795aa575c82453
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327599"
---
# <a name="wditlvipv4checksumoffload"></a>WDI\_TLV\_IPV4\_CHECKSUM\_OFFLOAD


WDI\_TLV\_IPV4\_校验和\_卸载是包含校验和卸载功能的 IPv4 TLV。

## <a name="tlv-type"></a>TLV 类型


0xCF

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                  |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------|
| [**WDI\_TLV\_CHECKSUM\_OFFLOAD\_V4\_TX\_PARAMETERS**](wdi-tlv-checksum-offload-v4-tx-parameters.md) |                                |          | 参数的 Tx 校验和卸载的 IPv4。 |
| [**WDI\_TLV\_CHECKSUM\_OFFLOAD\_V4\_RX\_PARAMETERS**](wdi-tlv-checksum-offload-v4-rx-parameters.md) |                                |          | 参数的 Rx 校验和卸载的 IPv4。 |

 

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

 

 




